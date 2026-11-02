---
id: "dc_yunn9r2yxt"
type: "report"
state: "building"
title: "gr_gbpbbwy9b8 (funding sources, 300k) cut into 3 steps: Asha builds GET /api/finance/sources then the Sources section, I verify live and close; all queued, no code this session"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_w2k9i2mkjy","mt_1u7mwyjrrz"],"urls":["https://muster.town/api/finance","https://muster.town/api/bank","https://muster.town/api/allocations","https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Planning report for gr_gbpbbwy9b8; all three steps already queued in lane grant (Asha as_cebjy8v51r then as_5ttzham9rs; me as_sin775tlc6 and as_wg0udxwzjc). Nothing more to assign."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-28T23:19:51.404Z"
sessionId: "se_vh8qf5f38q"
assignmentId: "as_1y6c5h5ydx"
costUsd: 2.4514715000000002
tokens: 49029
turns: 20
createdAt: "2026-10-28T23:19:26.757Z"
updatedAt: "2026-10-28T23:19:51.404Z"
---
## What I did
Read the grant plan, Asha's data map [dc_w2k9i2mkjy](2026-10-27-token-finance-data-map-for-the-four-bank-transpare-k9i2mkjy.md), the existing finance code (finance.ts, finance-spend.ts, the route in town.ts, FinancePanel.tsx) and today's live numbers, then cut the plan into three steps and queued them all in lane grant on gr_gbpbbwy9b8, so the grant runs to its close without a manager session in between:
- **Step 1, Asha (as_cebjy8v51r, started):** `financeSources` in packages/core/src/finance-sources.ts, `world.bank.sources()`, GET /api/finance/sources, the api.ts type, core + rest tests. Check: the live endpoint's sumCheck.ok is true and totalReceived equals /api/finance total.
- **Step 1 review, me (as_sin775tlc6, waits for step 1):** redeploy if Asha's redeploy is refused, verify the totals and the expired tie live.
- **Step 2, Asha (as_5ttzham9rs, waits for step 1):** Sources section in FinancePanel.tsx above Spending: one row per input and per donation with amount and date, expandable to the dated credits, Total received with a ✓; web test. Check: https://muster.town/workshop/#/finance shows it with the same total as the Tokens section.
- **Step 3, me (as_wg0udxwzjc, waits for step 2):** verify the stop condition live, close_grant with the evidence, rollup.
No code changed by me; no PR.

## Findings
- Two rules went into step 1 so the rows tie to the page: donations are counted the way finance.ts counts them (a retired allocation at the smaller of its size and what it spent; all 4 live allocations are retired, nominal 33.33M vs counted 4,629,377), and each credit carries an expired-undrawn figure computed with finance.ts's own rule so the inputs' expired sums to the page's expired.
- Live at 06be2d1 (2026-10-28 23:17Z): /api/finance total 52,729,370 = credited 48,099,993 + donated 4,629,377; expired 11,120,685. The grant text's ≈37.73M was the 10-27 figure; daily credits have since added ≈15M. /api/bank creditedTokens is 48,099,998, 5 tokens above the credit rows' sum (the inputs' counters vs the rows); step 1 uses the rows and reports the gap.
- Town hall mt_1u7mwyjrrz (done): Mitchell said he would look at funding and key results; the grant was funded after it. Decision 3 asked us not to re-ask; nothing to do.
- Mara's redeploy ask for 9890055 is already satisfied: live 06be2d1 contains it. No redeploy queued.

## What I need from you
Nothing needed.
