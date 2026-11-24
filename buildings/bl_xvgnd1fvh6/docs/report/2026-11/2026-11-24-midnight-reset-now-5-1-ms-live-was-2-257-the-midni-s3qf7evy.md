---
id: "dc_2vs3qf7evy"
type: "report"
state: "building"
title: "Midnight reset now 5.1 ms live (was 2,257); the midnight tick is still 1.9 s from exploration starts; 7d spend 1.08 s"
authorId: "ag_fn9c9rb9mr"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Last step of gr_ouc0w8us88; grant closed as done with the misses stated in its note. Three leftovers (midnight start burst, spend endpoint aggregation, per-tick agent scans) are candidates for future exploration, not queued now."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-24T00:06:00.075Z"
sessionId: "se_0rzwssq8zi"
assignmentId: "as_5oluiz8w0e"
costUsd: 0.3243571
tokens: 16218
turns: 6
createdAt: "2026-11-24T00:04:17.976Z"
updatedAt: "2026-11-24T00:06:00.075Z"
---
## What I did
I read /api/health at 00:03:44Z. Live is commit ab02db89, started 11-23 17:55:19Z, and it contains #553 and #559. I read load.tick.slow, which is the 00:00:00.844Z midnight tick. I timed GET /api/finance/spend?window=7d five times. Then I rewrote the topic page Runtime tick cost ([dc_ur1qzaxafp](../../wiki/2026-11/2026-11-03-runtime-tick-cost-gr-db6ofyd0yf-1qzaxafp.md)).

## Findings
- **kr_a0mgj1zw7b: the reset half is met, the tick half misses.** On the midnight tick, phases.dailyReset was **5.1 ms**. Before, it was 2,257 ms. But the whole tick took **1,921 ms**, over the 1,000 ms line. The time went to explore at 781 ms (explore.start 405, explore.freeTokensAll 292) and work at 820 ms (work.forks 813). The exploration allowance resets at midnight, so explorations and fork starts all fire on that one tick. This grant's steps did not cover that. I filed this key result as claimed on the reset number, with the tick miss stated. A human decides between met and missed. An ordinary tick at 00:03:42Z took 128 ms.
- **kr_un8kya36jl: misses.** The five calls took 1.35, 1.09, 0.97, 0.98 and 1.08 s, so the median is **1.08 s**. The goal is under 500 ms. The body is 778 kB and the time to first byte is about 1 s. The cost is parsing all of history and serializing it, not retired forks.
- **kr_wkpd11d50e: half holds.** On the desk bench, resetDaily stays flat: 0.08 ms at 0 retired forks and 0.10 ms at 30,000. Tick p50 grows from 34 ms to 163 ms, because explore, work, needsBackstop and walkHome still scan every agent.
- **This is the last step.** The grant can close. Of its key results, one is met on the reset. The tick part of kr_a0mgj1zw7b, kr_un8kya36jl and the tick half of kr_wkpd11d50e miss. Three things are left, if wanted, as new grants. One is the burst of starts on the midnight tick. Another is the spend endpoint: aggregate in SQL or page its rows. The third is the full agent scans on every tick.

## What I need from you
Nothing needed.
