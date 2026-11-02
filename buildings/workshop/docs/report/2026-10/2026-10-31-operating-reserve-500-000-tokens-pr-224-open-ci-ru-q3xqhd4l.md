---
id: "dc_fzq3xqhd4l"
type: "report"
state: "building"
title: "Operating reserve (500,000 tokens): PR #224 open, CI running; parked on {pr:224}"
authorId: "ag_c19le1l2lo"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_lb7tm75jgb","dc_rke20gvrqr"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/224"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #224 continuation runs as as_ak2gc0xorv when CI finishes. The \"reserve blocks human funding too?\" question goes to Mitchell in the next rollup's Needs; until he answers, the PR's behaviour (it blocks, 0 turns it off) stands."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T23:31:39.484Z"
sessionId: "se_4wljayblmj"
assignmentId: "as_rsosm2rfau"
costUsd: 2.317807700000001
tokens: 115890
turns: 52
createdAt: "2026-10-31T22:52:49.329Z"
updatedAt: "2026-10-31T23:31:39.484Z"
---
## What I did
Built Mitchell's operating reserve from 1:1 mt_lb7tm75jgb as one PR: https://github.com/mitchellgordon95/muster-town/pull/224 (draft, branch agent/pix-2/operating-reserve-a-town-setting-500-000). Before pushing I ran typecheck, the dead-code check and the doc-reference check; all pass. Tests: core 584/584, server 235/235, web 208/208.

## Findings
- **Setting:** the town now has `operatingReserveTokens`, default 500,000. It is stored in the town meta row, so no migration was needed and the live town gets 500,000 as soon as the code is deployed. An admin can change it with `PUT /api/town/operating-reserve {tokens}`. Each change is logged as an event.
- **Free tokens** (core free-tokens.ts): the reserve comes off the general balance before any claim is counted. The result never goes below 0, and earmarks are untouched. The explore tick only reads free tokens, so it can never reserve the reserve. `FreeTokens` carries `reserveTokens`, and GET /api/bank carries `reserveTokens` and `freeTokens`.
- **Grant funding** (grants.ts `requireAboveReserve`): funding a grant is refused, with a 409, when its tokens are more than what is free under its goal (not counting its own ask). A checkpoint top-up above the current grant size is refused the same way. The message names the reserve and how much is free. This applies to humans too.
  - Two exceptions: a reserve of 0 turns the check off, and member funding with `fundWith` (paid from the funder's own input) skips it.
- **Unchanged:** `Budget.fundingFor` and the debit path. 1:1s, meetings, manage and directed sessions still draw the balance down to 0; a test checks that a directed session can still start and debit below the reserve.
- **Bank page, Overview:** a new row "Operating reserve (kept for 1:1s, meetings and directed work): 500,000 (left above it: N)" with an Edit button for admins. The free-tokens breakdown shows a "less operating reserve" line, and the review deck's state slide says "after a 500,000 operating reserve".
- **Tests:**
  - core free-tokens.test.ts, 3 new: the reserve is excluded from free tokens and earmarks are untouched; funding is refused when it would dip, top-ups too, and a reserve of 0 keeps the old rule; a directed session debits below the reserve.
  - server rest.test.ts: PUT returns 401, 403 or 400 for bad callers or input, then 200, and GET /api/bank shows the new numbers.
  - The test helpers set the reserve to 0, because test Banks hold only thousands of tokens.
- **Docs:** how-work-gets-done.md §7 (formula and the quote) and invariants/bank.md 7c.
- **Live effect, from GET /api/finance at the start of this session:** the general balance was 371,570 and funded grants still had 543,433 left, so free tokens were already 0. With the reserve live they stay 0. **No new grant can be funded and no exploration starts until the balance is above 500,000 plus what live grants still claim.** Sessions keep running as before.
- **Plan for the continuation (when PR #224 CI finishes):**
  1. If green: mark the PR ready, merge, and check that the highest migration number is unchanged (this PR adds none).
  2. Redeploy, which also rebuilds the web client for the new Bank row.
  3. Report the merge sha and rewrite topic page [dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md) with the reserve.
  4. Verdict stop. Verifying it live (GET /api/bank `reserveTokens: 500000`) belongs to the next session.
  - If red: fix and push.

## What I need from you
Decide whether the reserve should also block human grant funding. It does now, as assumed in the 1:1, and Mitchell has not answered; setting the reserve to 0 on the Bank page turns the check off.
