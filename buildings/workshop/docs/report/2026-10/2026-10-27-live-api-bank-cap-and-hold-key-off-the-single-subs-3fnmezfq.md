---
id: "dc_iv3fnmezfq"
type: "report"
state: "building"
title: "Live /api/bank: cap and hold key off the single subscription input bi_upetwkezdm (15M adj./day, 58M/week); learned cap still null, hold dormant, 0 deaths since the 00:36Z clock; gr_iq5m7dug56 not yet continued (1,640,037 / 1,666,667 adj.)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_z4zgfk6tsz","dc_nwcbe7srkf","dc_ocko41bnrw"],"urls":["https://muster.town/api/bank","https://muster.town/api/grants/gr_iq5m7dug56"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Live check done; the grant continue/adjust is Mitchell's (goes into the next rollup's Needs)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T03:59:57.214Z"
sessionId: "se_wnbzuy2sar"
assignmentId: "as_kcbmhlpscr"
costUsd: 1.8665988000000002
tokens: 31329
turns: 15
createdAt: "2026-10-27T03:59:37.518Z"
updatedAt: "2026-10-27T03:59:57.214Z"
---
## What I did
Read the town-hall notes ([dc_z4zgfk6tsz](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zgfk6tsz.md), decision 1) and checked the live server at 04:10Z: GET /api/health, GET /api/bank and GET /api/grants/gr_iq5m7dug56, plus the cap code (packages/core/src/caps.ts, bank.ts getCap) to confirm the mechanism. No code change. Wiki "Bank accuracy grant" (dc_ocko41bnrw) rewritten and shortened.

## Findings
**Cap and hold key off the single input: verified.** The Bank picks the oldest non-cancelled subscription input; Mitchell cancelled every old input at 02:59Z and added one at 03:00Z, so there is exactly one.

| Live /api/bank `cap` at 04:10Z | value |
|---|---|
| inputId | bi_upetwkezdm ("Mitchell's subscription") |
| that input | 15,000,000 adj./day, weeklyCapTokens 58,000,000, next credit 03:00Z 10-28 |
| learnedCap / days | null / 0 (no bank.cap event yet) |
| spentToday (since 00:00Z) | 1,222,970 adj. |
| typicalSession | 17,430 adj. |
| held / reason | false / null, resets 00:00Z 10-28 |
| balance | 16,777,094 adj. |
| dailyInflow | 8,285,714 adj. (= 58M/7, the weekly cap binds, not the 15M daily figure) |

Two things to know when reading that: the input Mitchell entered is 15M/day, not 16M; and the learned cap is not read from the input's size at all. It is learned from where the subscription actually dies (median over 14 days of each day's lowest bank.cap spend), and the hold fires when today's subscription spend is within one typical session of it. Until the first cap death the hold stays dormant, which is the intended behaviour. The exploration allowance per building moved to 828,571 adj. (10% of the daily inflow) as a side effect of the new input.

**Deaths.** Rolling 7-day counter: 21 (10 cap + 11 budget-exhausted). Newest death 22:43Z 10-26 (Prod out of budget). Zero since the KR clock started at 00:36Z 10-27 (about 3.5 h in). Drift for 10-26: Fable 1.005 over 22 sessions, Sonnet 1.000 over 3.

**Grant gr_iq5m7dug56 is not yet continued or adjusted.** Still funded at 1,666,667 adj. with 1,640,037 spent (98.4%); the last human action is the adjust to 1,666,667 at 22:33Z 10-26, and the 100% checkpoint (rollup 13, [dc_nwcbe7srkf](2026-10-27-workshop-rollup-13-checkpoint-gr-iq5m7dug56-at-100-cbe7srkf.md)) is still pending, so grant-lane Bank sessions stay held. Historical ledgers: best effort, nothing to back-fill, as Mitchell said.

**Aside, not this assignment:** live commit is still df3daf5, so ec6ae2c (wake step 1) is not live yet even though my continuation as_xv4b99jffq resumed; that assignment handles it.

The figure above goes into rollup 16, which is the draft-format rollup assigned in as_3e2vfl920b.

## What I need from you
Continue gr_iq5m7dug56 from the Town Hall in-tray and adjust it to about 2,000,000 adj. tokens (decision 1 of the town hall); it is still at 1,666,667 with 98.4% spent.
