---
id: "dc_jvgqbh1h8j"
type: "report"
state: "building"
title: "gr_rdzg83m0al (runway counts inflow) cut into two chained fork steps: step 1 core + web + tests in one PR queued as as_vctbyzvmbb, step 2 signed-out live check with picture queued as as_mr6st1svdy"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_ulbwe2sdyf","dc_dw0izucnip"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Runway grant steps as_vctbyzvmbb and as_mr6st1svdy are on the queue; I close gr_rdzg83m0al from step 2's report."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T21:03:53.913Z"
sessionId: "se_xtdvmwumwg"
assignmentId: "as_tki5frl10t"
costUsd: 2.5970398500000003
tokens: 51941
turns: 16
createdAt: "2026-10-31T21:02:10.430Z"
updatedAt: "2026-10-31T21:03:53.913Z"
---
## What I did
Read the findings ([dc_ulbwe2sdyf](../../note/2026-10/2026-10-31-findings-the-bank-s-next-30-days-says-the-tokens-l-bwe2sdyf.md)) and the current code: the projection in packages/core/src/finance.ts:116-131 has no inflow, `Bank.dailyInflow()` (bank.ts:680) already applies the weekly-cap/7 rule, and the web `runwayDays` helper in BankFinance.tsx:31 divides `left` by the trailing burn, so it reads 0 days. Cut the grant (160,000 tokens; this session charged to it) into two fork sessions instead of the plan's three, so the live check still fits before the 100% checkpoint:

- **Step 1, as_vctbyzvmbb (building queue, lane grant):** core + web + tests in one PR, merged on green. Projection gains `dailyInflow` (via a shared `dailyInflowOf(inputs)` that `Bank.dailyInflow()` also calls, so `/api/bank dailyInflowTokens` and `/api/finance projection.dailyInflow` can never differ), `netDailyBurn`, `projectedInflow30d`, `runwayDays` (null when covered or no usage) and `runway: "covered" | "days" | "no-usage"`. ProjectionView rows: Burn / Coming in / Net per day / Projected use / Tokens left last ("covered by the daily inflow"). Mock, web test, core tests (covered, short, no usage, cancelled/once inputs excluded, weekly cap bounds a subscription), and the identity added to `npm run check:finance`. Pages attached: [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md), [dc_bac7ir715s](../../wiki/2026-10/2026-10-29-finance-endpoint-pattern-code-c7ir715s.md), [dc_a0q82pir2r](../../wiki/2026-10/2026-10-29-deploy-ci-and-push-for-bank-transparency-q82pir2r.md).
- **Step 2, as_mr6st1svdy (waits on step 1):** signed out at muster.town, GET /api/finance and /api/bank numbers in a table, Overview "Next 30 days" must read "covered by the daily inflow" with today's inflow 10.0M/day against burn ~8.5M/day, one cropped picture; parks on {deploy: sha} if the merge isn't live. Pages: [dc_xeui247glt](../../wiki/2026-10/2026-10-29-finance-page-pictures-and-layout-checks-ui247glt.md), [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md), [dc_a0q82pir2r](../../wiki/2026-10/2026-10-29-deploy-ci-and-push-for-bank-transparency-q82pir2r.md).

I close the grant from step 2's report (close_grant + rollup with both reports in provenance). Topic page [dc_slumnj2s4z](../../wiki/2026-10/2026-10-29-bank-transparency-key-results-and-grants-umnj2s4z.md) rewritten (it was 20 h stale); my wiki and log updated.

## Findings
- Budget: the previous grant's fork steps cost 60,466 (core) and 72,770 (web) adj. tokens; three steps plus this session would overrun 160,000 and hold the live check at the checkpoint. Two steps should land at roughly 100,000–130,000.
- Weekly cap: per the 1:1 (mt_p3ge56kg03) it is folded into inflow per day, as `Bank.dailyInflow` already does; no separate line. Display and projection only, no debit, credit or ledger change, so nothing to ask first under the merge rules ([dc_57nuw740sc](../../fyi/2026-10/2026-10-27-merge-rules-for-bank-transparency-revised-2026-10-nuw740sc.md)).
- Not part of this grant: gr_wp2rg302qu is at its checkpoint (155,864 / 150,000), so step 2b as_7peyu8d7y6 stays held until Mitchell decides on the checkpoint in his in-tray.

## What I need from you
Nothing needed.
