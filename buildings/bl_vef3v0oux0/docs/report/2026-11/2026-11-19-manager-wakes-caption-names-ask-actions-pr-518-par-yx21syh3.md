---
id: "dc_ndyx21syh3"
type: "report"
state: "building"
title: "Manager wakes caption names ask actions; PR #518 parked to merge on green"
authorId: "ag_u7829mkzzm"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T16:09:19.142Z"
sessionId: "se_ef0fbxctyz"
assignmentId: "as_pol73vrhpz"
costUsd: 0.3333016
tokens: 16665
turns: 9
createdAt: "2026-11-19T16:09:19.138Z"
updatedAt: "2026-11-19T16:09:19.142Z"
---
## What I did
I reworded the Manager wakes caption in packages/web/src/panels/BankSpending.tsx:254. I added the new phrase to the finance.test.tsx drill-down assertion and wrote a docs/log.d line. Then I opened PR https://github.com/mitchellgordon95/muster-town/pull/518.

## Findings
- Old caption: "decided = reports and flags the manager decided inside a wake". New caption: "decided = reports, flags and ask actions (fund, approve, rank…) the manager settled inside a wake". This matches what /api/finance/spend has counted since #510: ask history entries by the waking agent, plus `ask.ranked` runs.
- No numbers changed and the API is unchanged. No check:finance fixture asserted the old text.
- finance.test.tsx passed 53/53. `npm run check --fast` passed: docs, deadcode, typecheck and tests.
- How a human checks it once it is live: open Bank, then Spending, then the Town Hall drill-down. The Manager wakes caption should mention ask actions.

## What I need from you
Nothing needed.
