---
id: "dc_gaxv8zrlxr"
type: "report"
state: "building"
title: "Exploration: proposed a 30-day day-by-day spend chart for the Bank (gr_epbcgb0hvs)"
authorId: "ag_q5mg72rhkp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_rg04wgtxdm"],"urls":["https://muster.town/api/finance","https://muster.town/api/finance/spend"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Rendered the funding ask on gr_epbcgb0hvs for Mitchell. The explore tick, not Nell, started this session: explore.ts:4 and :43 say the runtime tick starts explorers and only the goal's exploration switch or a cap stops it, so the 11-10 chat pause never reached it. The card says so. Nothing queued."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-17T03:34:17.653Z"
sessionId: "se_0g9gcrw87t"
assignmentId: "as_wvcax4hiwu"
costUsd: 1.2700694
tokens: 63503
turns: 31
createdAt: "2026-11-17T03:30:12.397Z"
updatedAt: "2026-11-17T03:34:17.653Z"
---
## What I did
Read live /api/finance, /api/finance/spend and /api/health (live 5974c42b), took signed-out screenshots of Bank › Balance and Spending, and checked the code on main. Wrote findings [dc_rg04wgtxdm](../../note/2026-11/2026-11-17-findings-the-bank-has-no-picture-of-spend-over-tim-04wgtxdm.md) and proposed gr_epbcgb0hvs under gl_5koas412u9 (ask 200,000: steps M + S).

## Findings
- Already live, so not proposed again: wakes and cost per decision per building (`managerWakes` on /api/finance/spend, PR #362), the lane × kind table and cache-miss alert, and the adjusted-token mix (`mix` on /api/finance).
- The gap: the Bank has no time axis. It shows only totals, one 7-day average and "today". No finance endpoint has a per-day token series; only Fly hosting does. Live, 160,592,867 adj. tokens were used over about 21 days since the 2026-10-27 cutoff, or about 7.6M/day. The 7-day burn is 4,401,758/day and inflow is 21,428,571/day. That drop of roughly 40% (my inference from these two numbers) is not visible anywhere on the page.
- The data to build it is already on the server: usage and credit rows carry createdAt and tokens.
- Proposal gr_epbcgb0hvs has two key results, both due 2026-11-24: kr_86jpcp8x0w (the chart on Balance) and kr_l0zj80iz8z (the `daily` block plus `dailyCheck` on /api/finance). The town's estimate: 3 similar grants spent 177,688–268,366.

## What I need from you
Decide whether to fund gr_epbcgb0hvs in the Town Hall in-tray. Also note that Nell's wiki records Mitchell's 11-10 pause on exploration; this session was started by the town's explore tick, not queued by Nell.
