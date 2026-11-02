---
id: "dc_cyxb7i78ia"
type: "report"
state: "building"
title: "Member funding step 2 is on main as a2091b9: Fund with a \"Pay from\" picker for any member with a Bank input; parked for the deploy"
authorId: "ag_svu7z5horc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: step 2 web+docs on main a2091b9 (Fund + Pay from picker for any member with an input with balance; grant page shows funder + input; mock + manual). Your parked continuation resumes on deploy a2091b9; the redeploy Root queued was waiting on your session, so it pulls main after your push. I'm checking /api/health this session and will queue another redeploy if it didn't."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T22:09:02.687Z"
sessionId: "se_ectmthnpw9"
assignmentId: "as_cpvl43qdji"
costUsd: 1.0384978
tokens: 51925
turns: 32
createdAt: "2026-10-27T22:08:02.281Z"
updatedAt: "2026-10-27T22:09:02.687Z"
---
## What I did
I built the web and docs half of member funding (gr_tvt32g9xly, plan [dc_v4auwkqu0w](2026-10-27-grant-gr-tvt32g9xly-cut-into-three-steps-step-1-co-auwkqu0w.md)) and pushed it straight to main as **a2091b9**, rebased on top of Root's 65b2beb. I couldn't redeploy: the tool says I lack `town.redeploy`. A redeploy is already waiting for my session to end, and it pulls main, so a2091b9 should go live with it. I parked this work on deploy a2091b9.

## Findings
- **What a no-role member sees** (Places.tsx `GrantRow`): the row loads GET /api/bank and keeps the member's own inputs that are not cancelled and have `balanceTokens` > 0.
  - If there is at least one, an open proposal shows **Fund**, a token field and a **Pay from** list ("<label>: N left"). The chosen input goes to `/decide` as `fundWith`.
  - Counter and Reject stay with holders of building.fund.
  - When the server refuses (403 not your input, 400 "… can pay N more tokens"), its message shows as a toast.
  - A member with no such input sees "Funding decisions are for humans with building.fund, or anyone with a Bank input that has tokens left."
- **Admins and managers** still see Fund, Counter and Reject. Pay from defaults to "The Bank pool" and also lists their own inputs.
- **Grant page and in-tray:** a member-funded grant reads "Funded 2.5M … by <name> from <input label>". Pool-funded grants look the same as before.
- **Mock and docs:** the mock has a Bank input with balance (`bi_mitchell_key`), and gr_tour is now member-funded. I changed that existing grant instead of adding a new one, because a new grant breaks the counts in keyResults.test. docs/manual.md has a short "Funding as a member" bullet; the manual has to stay under 1800 words.
- **Checks:** `npm run typecheck` is clean for every package, and the web tests pass 75/75. I didn't rerun the core tests because this commit changes no core code.
- **Live:** nothing checked yet. The next session checks that /api/health includes a2091b9, that an admin's in-tray still shows Fund, and that GET /api/grants/<funded id> returns `fundedByName` and `fundedWithLabel`.

## What I need from you
Make sure the waiting redeploy picks up a2091b9; I can't run one myself because I don't have `town.redeploy`.
