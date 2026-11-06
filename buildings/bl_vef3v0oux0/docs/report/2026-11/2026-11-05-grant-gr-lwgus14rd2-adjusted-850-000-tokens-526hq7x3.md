---
id: "dc_uz526hq7x3"
type: "report"
state: "building"
title: "Grant gr_lwgus14rd2 adjusted: 850,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:128374:bl_vef3v0oux0"]
decision: "approve"
decisionNote: "Taken in: gr_lwgus14rd2 continued at 850k, kr_f49co6lg51 redefined around prefix busting. The directed as_es824n3ryo had already run (PR #364 open); its directed continuation as_0o6p2lgor6 is cancelled and re-queued under the grant."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-05T20:01:11.377Z"
createdAt: "2026-11-05T19:31:33.182Z"
updatedAt: "2026-11-05T20:01:11.377Z"
---
Written by the town: Mitchell adjusted grant gr_lwgus14rd2 at its checkpoint (event 128374, 2026-11-05 19:31 UTC).

## Summary

Grant gr_lwgus14rd2 "Token cost is legible and watched: the Bank shows spend by lane × token kind, counts manager wakes per building, and raises a HUD alert when a session purpose re-writes its cached prefix every wake." adjusted by Mitchell: 850,000 tokens.

Status funded; 734,638 of 850,000 tokens spent; key results kr_pzr1fkgas8 [claimed] Bank → Spending shows a lane × token-kind table (grant, exploration, directed, retainer, manager) × (input, output, cache read, cache write 5 min, cache write 1 h) for today and 7 days, in adj. tokens and ≈ $, with the cache-write share of cost per lane; drill-down per building.; kr_f49co6lg51 [on-track] A system event `alert: cache-miss` (one per day per session purpose) fires when the 1-hour cache-write share of a purpose's cost over the day passes 20%, or a session's first-turn cache write exceeds its cache read; the HUD shows it like the funding alerts, with the sessions it saw.; kr_avafh64h02 [not-started] The Bank shows manager wakes per building per day beside their cost (wakes, adj. tokens, cost per wake and per decided report), so four wakes in fifteen minutes for four reports is a visible number..

The note: by Mitchell via Secretary in mt_pr3347g2w2: "the first please"
Topped up by 250k (600k → 850k), as Nell asked at the checkpoint. kr_f49co6lg51 is redefined (decision 3 of mt_pr3347g2w2): the daily alert measures prefix busting, not cache-write share. Per session, for turns 2+: re-write rate = cache_creation / (cache_read + cache_creation) per turn; a session busts when that rate is high on most of its turns; the alert fires on the share of busting sessions per purpose per day, naming the worst session ids. The 1 h cache-write share of cost stays as a Spending column, not an alert. The 20% threshold question is dropped. Directed assignment as_es824n3ryo is superseded by this grant work: cancel it.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
