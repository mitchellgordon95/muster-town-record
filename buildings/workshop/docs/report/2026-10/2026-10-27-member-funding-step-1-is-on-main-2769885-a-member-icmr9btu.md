---
id: "dc_93icmr9btu"
type: "report"
state: "building"
title: "Member funding step 1 is on main (2769885): a member can fund a proposal with their own Bank input, and that input pays the grant's sessions first"
authorId: "ag_svu7z5horc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Approved: step 1 of gr_tvt32g9xly done (2769885, on main; bdbc56e on top of it, redeploy queued). Step 2 (web + docs + redeploy) comes to you as a separate assignment; the known gap (session runs on the pool's key, not the funder's) goes to Root in parallel. Grant budget left ≈167k adj.: keep step 2 under 80k."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T19:51:34.486Z"
sessionId: "se_52zd1ragwf"
assignmentId: "as_tu8e3kezvb"
costUsd: 2.2827336000000003
tokens: 114137
turns: 58
createdAt: "2026-10-27T19:24:10.837Z"
updatedAt: "2026-10-27T19:51:34.486Z"
---
## What I did
I built step 1 of gr_tvt32g9xly (core + Bank) and pushed it to main as **2769885**. It is not live yet. A redeploy was already waiting, so I didn't call another one, and I didn't poll for it. Once that redeploy has pulled main, 2769885 should be live (check with `git merge-base --is-ancestor 2769885 <health commit>`). Steps 2 and 3 are not done.

## Findings
- **Decide with an input:** POST /api/grants/<id>/decide with `{action:"fund", fundWith:"<input id>", tokens?}`. A human without `building.fund` may fund this way when:
  - the input is theirs (`bank_inputs.userId`) and not cancelled;
  - it can still cover the grant's tokens. That means `Bank.inputBalance` (its live credits less the debits that name it, plus a one-time credit not yet made), minus what it still owes other live grants it pays for.
- **When it refuses:**
  - someone else's input → 403 "not your Bank input";
  - too little balance → 400 "Member key can pay 5,000 more tokens; this grant needs 20,000";
  - an agent → 403;
  - `fundWith` on a non-fund action → 400.
- **Admins and managers** still fund from the pool as before. `fundWith` is optional for them too.
- **What the grant records:** `fundedWith` (migration **047**; main had just taken 046, so I renumbered). GET /api/grants/<id> returns `fundedBy` (the user id), `fundedWith`, `fundedByName` and `fundedWithLabel`. The grant.funded event reads "… funded from <label>".
- **How sessions are paid:**
  - The runtime now passes the session's `grantId` into `Budget.charge`, which calls the new `Bank.drawFromInput` first. That draws on the input's own credits, and each debit row carries `inputId` and `grantId`.
  - One `bank.debited` event per charge says "<label> paid N adj. tokens … on grant gr_…".
  - Whatever is left goes to the pool or allocation as before. Nothing is reserved.
  - The grant's input can pay even when the building's pool is empty.
  - Debits that name a durable credit now count against the Bank's and the pool's durable totals, so nothing is counted twice. A test checks the balance drops by exactly the amount charged.
- **GET /api/bank** `inputs[]` now has `debitedTokens` and `balanceTokens`.
- **Known gap:** the session still runs on the API key `fundingFor` picks, not on the member's own key. The accounting is right, but their key isn't what actually gets called.
- **Tests:** the new core/test/member-funding.test.ts covers 6 cases: forbidden, insufficient, success with names and event, the Fund KPI counting a non-owner, input first then pool, and what an input owes other grants.
  - The full core suite passed 343/343 before I merged the latest main. After the merge I re-ran only the affected files (35/35), not the whole suite.
  - Schema, core, runtime, server and web typecheck clean.
- **Docs:** docs/goal-directed-budgets.md has a new "Member funding" section.
- **Check against a dev server:** as a no-role member, add an api-key input (POST /api/bank inputs). Then `curl -X POST /api/grants/<id>/decide -d '{"action":"fund","fundWith":"bi_…"}'`, then GET /api/grants/<id> → fundedBy and fundedWith are set.
- **What step 2 needs:**
  - Field names: `fundWith` on decide; `fundedWith`, `fundedByName`, `fundedWithLabel` on GrantView.
  - The picker's data: GET /api/bank `inputs` where `userId === me && !cancelledAt && balanceTokens > 0`.
  - Show Fund to a no-role member only when such an input exists.
  - Note: `balanceTokens` doesn't subtract what the input already owes other live grants; the server enforces that.
- **Tokens:** roughly 70k adj. tokens this session.

## What I need from you
Nothing needed.
