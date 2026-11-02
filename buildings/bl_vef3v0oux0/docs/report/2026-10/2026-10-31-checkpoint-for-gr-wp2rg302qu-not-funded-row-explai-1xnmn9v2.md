---
id: "dc_sj1xnmn9v2"
type: "report"
state: "building"
title: "Checkpoint for gr_wp2rg302qu (Not funded row explains itself) is moot: Mitchell raised the grant to 300,000 four minutes after it fired; no checkpoint filed, work continues (steps 2b and 3 queued)"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_vs2irbg8um","dc_3cuhr9j0we","dc_vurxxsq1tu","dc_ltb8hesjzj"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Correct call: the checkpoint assignment outlived its trigger (Mitchell raised gr_wp2rg302qu to 300,000 four minutes after it fired). Not filing checkpoint_grant kept steps 2b (as_7peyu8d7y6) and 3 (as_qik35m0gtu) unblocked. Close rollup follows step 3's report."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T21:07:32.386Z"
sessionId: "se_8ta6ae4678"
assignmentId: "as_4kik454m9h"
costUsd: 2.1652360500000003
tokens: 43305
turns: 13
createdAt: "2026-10-31T21:07:06.402Z"
updatedAt: "2026-10-31T21:07:32.386Z"
---
## What I did

Read the grant's history before writing anything. The 100% checkpoint on gr_wp2rg302qu fired at 20:55:55Z (155,864 of 150,000 adj. tokens, 104%). Mitchell adjusted the grant to 300,000 at 20:59:42Z ([dc_vs2irbg8um](2026-10-31-grant-gr-wp2rg302qu-adjusted-300-000-tokens-2irbg8um.md), which I approved at 21:03Z). The grant is `funded`, 155,864 / 300,000 (52%), `checkpointsDone` empty, nothing held. So I did **not** call `checkpoint_grant`: it sets the key result's status and then holds the grant until a human continues, adjusts or cuts it, which would re-block steps 2b (as_7peyu8d7y6) and 3 (as_qik35m0gtu) that Mitchell's adjustment just released. I also filed no rollup: the last one was 17 minutes ago, Mitchell already decided the checkpoint, and the stop condition is not met yet; the close rollup follows step 3 as planned. Recorded the live evidence below, rewrote my wiki (dc_ikm62c1s7y) and the topic page [dc_slumnj2s4z](../../wiki/2026-10/2026-10-29-bank-transparency-key-results-and-grants-umnj2s4z.md), logged the decision.

## Findings

Live commit 36a8a86 at 21:05Z, signed out, GET /api/finance/spend:

| Field | Value (adj. tokens) |
|---|---|
| notFunded | 195,957 (unchanged since 2026-10-29) |
| notFundedSplit: Town Workshop | 4,269,596 (5 usage rows) |
| notFundedSplit: Onboarding | 535,569 (3 rows) |
| notFundedSplit: Prod | 123,238 (3 rows) |
| notFundedSplitCheck | sum 4,928,403 vs 195,957, ok **false** |
| notFundedAllocationPaid | 4,269,596 |
| notFundedLastAt | 2026-10-26T22:52:13Z |

Against the testing plan:
- **Split sums to notFunded:** fails live. The Workshop figure equals its allocation-paid usage exactly: Budget.charge with an allocationId skips bank.drawTokens (packages/core/src/budget.ts:279-288), so allocation-paid usage has no debit and the 2 s rule counts it unpaid. Step 2b (queued, pending) excludes it and nets the rest, or carries a `reason`.
- **Note says cause, stop date, buildings, write-off:** merged in PR #196 (b53814f, on main) but **not yet live** at 36a8a86; step 3 checks it signed out and parks on the deploy if needed.
- **Row stopped growing:** holds. 195,957 on 10-29, 10-30 and 10-31; schedule sc_qu4lpdmgng re-checks at 03:00Z on 11-01 and 11-02.

Key result kr_jksobb0bwo reads as on-track by this evidence, but I left its status untouched because the only tool that sets it also re-holds the grant. Spend: 155,864 of 300,000 (the grant can take about 144,000 more, enough for 2b and 3).

Rule for next time (now on both pages): a "Write the checkpoint" assignment can outlive its trigger; read GET /api/grants/<id> history first and skip `checkpoint_grant` if a human already adjusted or continued it.

## What I need from you

Nothing needed.
