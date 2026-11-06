---
id: "dc_626291r1xr"
type: "report"
state: "building"
title: "Grant gr_lwgus14rd2 adjusted: 2,000,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:136498:bl_vef3v0oux0"]
decision: "approve"
decisionNote: "Taken in: gr_lwgus14rd2 continues at 2,000,000 tokens (1,121,467 spent). Nell 2 is already running on it (as_ail5blil47); no new work needed beyond what is queued."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-06T04:22:47.189Z"
createdAt: "2026-11-06T04:20:06.152Z"
updatedAt: "2026-11-06T04:22:47.189Z"
---
Written by the town: Mitchell adjusted grant gr_lwgus14rd2 at its checkpoint (event 136498, 2026-11-06 04:20 UTC).

## Summary

Grant gr_lwgus14rd2 "Token cost is legible and watched: the Bank shows spend by lane × token kind, counts manager wakes per building, and raises a HUD alert when a session purpose re-writes its cached prefix every wake." adjusted by Mitchell: 2,000,000 tokens.

Status funded; 1,121,467 of 2,000,000 tokens spent; key results kr_pzr1fkgas8 [claimed] Bank → Spending shows a lane × token-kind table (grant, exploration, directed, retainer, manager) × (input, output, cache read, cache write 5 min, cache write 1 h) for today and 7 days, in adj. tokens and ≈ $, with the cache-write share of cost per lane; drill-down per building.; kr_f49co6lg51 [on-track] A system event `alert: cache-miss` (one per day per session purpose) fires when the 1-hour cache-write share of a purpose's cost over the day passes 20%, or a session's first-turn cache write exceeds its cache read; the HUD shows it like the funding alerts, with the sessions it saw.; kr_avafh64h02 [on-track] The Bank shows manager wakes per building per day beside their cost (wakes, adj. tokens, cost per wake and per decided report), so four wakes in fifteen minutes for four reports is a visible number..

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
