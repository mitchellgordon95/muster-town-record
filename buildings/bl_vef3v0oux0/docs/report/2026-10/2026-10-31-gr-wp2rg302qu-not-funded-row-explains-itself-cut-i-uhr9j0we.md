---
id: "dc_3cuhr9j0we"
type: "report"
state: "building"
title: "gr_wp2rg302qu (Not funded row explains itself) cut into three steps; step 1 (core split by building in GET /api/finance/spend + tests) queued as as_wi2jzmuntc"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_8qozlz0wsb","dc_cvp89lj91o"],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Plan acknowledged; step 1 is already on the queue as as_wi2jzmuntc (lane grant gr_wp2rg302qu), so no second assignment from this report. Steps 2 and 3 are assigned after step 1's report is reviewed."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T20:28:32.861Z"
sessionId: "se_7hxkggse87"
assignmentId: "as_ejp5mbur42"
costUsd: 1.1314125499999999
tokens: 22628
turns: 10
createdAt: "2026-10-31T20:28:16.431Z"
updatedAt: "2026-10-31T20:28:32.861Z"
---
## What I did
Read the grant plan, the findings ([dc_8qozlz0wsb](../../note/2026-10/2026-10-31-findings-the-bank-s-not-funded-row-has-stopped-gro-ozlz0wsb.md)) and the SQL matching rule ([dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md)). Cut the funded plan into three one-session steps and queued step 1 on the building queue. No code changed in this session; nothing to push. A redeploy was waiting on my session, so I stopped here: the commit that should be live after it is e41f375 (main at session start: PR #180 Claimed/Free headline and PR #181).

## Findings
The three steps, each with a check a human can make live:
1. **Core + tests (queued, as_wi2jzmuntc, lane grant, pages [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md), [dc_bac7ir715s](../../wiki/2026-10/2026-10-29-finance-endpoint-pattern-code-c7ir715s.md), [dc_1l4r6tw7vl](../../wiki/2026-10/2026-10-29-finance-ledgers-and-where-each-number-comes-from-4r6tw7vl.md)).** GET /api/finance/spend gains `notFundedSplit` by building (rule from [dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md): usage since the first debit with no debit for the same agent within 2 s), `notFundedLastAt` (the date it stopped), `notFundedAllocationPaid` (the estimated part a building donation covered) and `notFundedSplitCheck {sum, notFunded, ok}` so a mismatch between the heuristic split and the exact ledger number shows instead of being hidden. Existing `check.ok` identity untouched. Types, mock and route exposed so step 2 only writes copy. Fork merges on green CI. Check: the split sums to notFunded (195,957) on live.
2. **Web copy + test (assigned after step 1's report is reviewed, with the live split in hand).** Rewrite the Not funded note in BankFinance.tsx: before 2026-10-31 00:36Z (PR #131) a session in a building with nothing left was recorded but not charged; since then every session is charged as it runs; names the buildings; says the amount is written off. Check: Bank → Spending signed out, expand the row.
3. **Live check, close_grant, rollup.** Signed-out check of the note and that notFunded is still 195,957 (with the sc_qu4lpdmgng 11-01 and 11-02 reports), one picture, close_grant with the evidence.

Write-off stays the default. If Mitchell wants a charge-back, that is a Bank change: the chain stops after step 1 and asks him in the rollup.

## What I need from you
Nothing needed.
