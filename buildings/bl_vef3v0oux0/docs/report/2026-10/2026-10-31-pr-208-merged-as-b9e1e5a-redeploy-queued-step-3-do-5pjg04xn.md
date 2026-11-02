---
id: "dc_hr5pjg04xn"
type: "report"
state: "building"
title: "PR #208 merged as b9e1e5a, redeploy queued; step 3 does the live check"
authorId: "ag_qrq0ihx9v3"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #208 merged as b9e1e5a, redeploy queued. Step 3 (as_0q37kh9x7c) does the live check once b9e1e5a is live and parks on {deploy: b9e1e5a} if not; it then rewrites dc_tkzoy81p4b. kr_518ed152d2 likely missed (split 658,807 vs notFunded 195,957): Mitchell's call at close, noted for the close rollup."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T22:19:30.340Z"
sessionId: "se_i7a4dw05q4"
assignmentId: "as_ukr52c9u8g"
costUsd: 0.32995749999999996
tokens: 16498
turns: 8
createdAt: "2026-10-31T22:17:20.219Z"
updatedAt: "2026-10-31T22:19:30.340Z"
---
## What I did
- PR #208 CI passed on head a4b8b8d (`check` SUCCESS). The head also merged cleanly into current main (98a9fac).
- I merged it: https://github.com/mitchellgordon95/muster-town/pull/208, merge commit **b9e1e5a**.
- I queued a redeploy. Live was ae18eb3 at 2026-10-31T22:16:54Z. The merge is not live yet.

## Findings
- I did not read GET /api/finance/spend or rewrite [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md), because b9e1e5a is not live yet. Parking this session a third time only to do that would duplicate step 3 (as_0q37kh9x7c), which starts once this assignment finishes. Step 3 does the signed-out live check and parks on {deploy: b9e1e5a} if needed.
- For step 3, check these once live is at b9e1e5a or later (`git merge-base --is-ancestor b9e1e5a <live commit>`):
  - Workshop no longer appears in `notFundedSplit`.
  - `notFundedAllocationPaid` is 4,269,596.
  - The split is Onboarding 535,569 and Prod 123,238, totalling 658,807. That does not equal `notFunded` 195,957, so `notFundedSplitCheck.ok` should be false.
  - `reason` should be present and shown as the plain note line.
  - Then rewrite [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md) with the live values.
- kr_518ed152d2 ("adds up exactly") will most likely be missed: `notFunded` = booked − used, while the split is a heuristic over undebited usage rows. Mitchell decides at the close.

## What I need from you
Nothing needed.
