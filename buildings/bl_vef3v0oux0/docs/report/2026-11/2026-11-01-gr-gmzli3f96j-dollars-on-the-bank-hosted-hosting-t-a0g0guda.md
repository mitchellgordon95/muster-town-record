---
id: "dc_kca0g0guda"
type: "report"
state: "building"
title: "gr_gmzli3f96j (dollars on the Bank, hosted Hosting tab) cut into three chained fork steps: step 1 core + web usd in one PR queued as as_el2651coa4, step 2 hosted Hosting fix as as_rv1tk0dogj, step 3 signed-out live check as as_4g9gnjipoe"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_gd8yuqk7t9","dc_8ce0993ntq","dc_slumnj2s4z"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "My own cut of gr_gmzli3f96j into three chained steps (as_el2651coa4 → as_rv1tk0dogj → as_4g9gnjipoe); step 1 is running on Nell 2. Next action is on step 3's report: read the three diffs, close_grant, roll up."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-01T02:04:38.707Z"
sessionId: "se_m6mqheshe0"
assignmentId: "as_cd0ivot8s3"
costUsd: 3.0477925499999996
tokens: 152390
turns: 19
createdAt: "2026-11-01T02:04:12.262Z"
updatedAt: "2026-11-01T02:04:38.707Z"
---
## What I did
Read the grant's findings ([dc_gd8yuqk7t9](../../note/2026-11/2026-11-01-findings-the-bank-shows-tokens-but-no-dollars-and-8yuqk7t9.md)) and the finance code it touches (core bank.ts price table and `bankModelOf`, finance.ts, finance-spend.ts, finance-fly.ts, server routes/town.ts, web BankFinance.tsx), then cut the plan into three steps and queued them on the building queue in lane grant (grantId gr_gmzli3f96j), chained with waitFor so each starts when the one before is done. Nothing was taken by me: each step is one fork session with its own token cap so the three fit the 300,000 stop condition. Rewrote the grants topic page [dc_slumnj2s4z](../../wiki/2026-10/2026-10-29-bank-transparency-key-results-and-grants-umnj2s4z.md) and my wiki; logged.

## Findings
- **Step 1, as_el2651coa4** (pages [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md), [dc_bac7ir715s](../../wiki/2026-10/2026-10-29-finance-endpoint-pattern-code-c7ir715s.md), [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md); cap 150,000): one PR. GET /api/finance gets a `usd` block (used, left, burnPerDay, inflowPerDay, pricedAt "api-list"); `used` priced per session at its own booking model so pre-076 Fable sessions count at $50/M, left/burn/inflow at BANK_MODEL's $20/M. /api/finance/spend rows carry `usd`, plus a dollar `usdSumCheck` on the same identity as the token one. Web: "≈ $X" on the four Overview rows, one footnote ("at API list price; a subscription pays a flat fee instead"), "$X" per building on Spending with a ✓ sentence; mock, tests, docs, check:finance. The fork parks on {pr: N}, merges on green, queues the redeploy. Covers kr_ct7jyhctu7 and kr_xiwj6gon7n.
- **Step 2, as_rv1tk0dogj** (waits on step 1; cap 120,000): routes/town.ts passes townOnFly false when `world.host.hosted`; finance-fly.ts returns `townPaidBy: "self" | "host"`, townUsd 0 and a window from the collective's creation for a hosted World (hosted flag passed as an option, not read from the env); the Hosting tab shows "The server is run by muster.town; this collective pays only for its own desks." Covers kr_cex3fn2g3t.
- **Step 3, as_4g9gnjipoe** (waits on step 2; pages [dc_xeui247glt](../../wiki/2026-10/2026-10-29-finance-page-pictures-and-layout-checks-ui247glt.md), [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md), [dc_a0q82pir2r](../../wiki/2026-10/2026-10-29-deploy-ci-and-push-for-bank-transparency-q82pir2r.md); cap 80,000): parks on {deploy: sha} if step 2 is not live, then signed-out checks on muster.town/#/bank (Overview dollars, footnote, Spending $ and ✓ line, usd.used equal across the two endpoints within $0.01) and muster.town/hollyville/#/bank (no Town Machine, townPaidBy "host", townUsd 0), the Workshop's Hosting unchanged, check:finance N/N, one cropped picture, topic pages rewritten. No code fixes in that step.
- **Next step for me:** when step 3's report lands with all three key results reading true, read the three diffs, close_grant with the evidence, and roll up with the three reports in sourceIds. If Mitchell objects to list-price dollars on a subscription-funded town, cancel step 1's web half and keep step 2 (the stop condition's "ship only the hosted Hosting fix").
- Live at this read: 7ca64bc (/api/health startedAt 02:02:37Z); main f5e72bf. Nothing of this grant is on main yet. PR #221 (Not funded copy) has its CI check passed; its merge continuation as_qno3pcrexh is pending and will run on its own.

## What I need from you
Nothing needed.
