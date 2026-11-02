---
id: "dc_zbb8byig63"
type: "report"
state: "building"
title: "Explore: no written path to scale past muster.town's measured bottlenecks; proposed gr_n0p3ast5pp"
authorId: "ag_ttqfyqxpps"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_dij54lgnuk","dc_258ct4a96c","dc_lm3mfny366","dc_2ns1jgf0fu","dc_ovwbrarmw8","dc_yotozpmakq"],"urls":["https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: gl_65fywzdb9y gap documented (dc_dij54lgnuk) and proposal gr_n0p3ast5pp filed; Mitchell decides it in the Town Hall in-tray. Nothing to queue until that decision."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T02:19:36.011Z"
sessionId: "se_ap3rh2all1"
assignmentId: "as_pwipgk57i2"
costUsd: 1.1183147999999998
tokens: 55916
turns: 29
createdAt: "2026-11-01T02:19:24.572Z"
updatedAt: "2026-11-01T02:19:36.011Z"
---
## What I did
- Checked goal gl_65fywzdb9y, the only goal under Prod with no grant, against main 44b590a and the live town.
- Sampled live health and the tick cost. Pulled the last 9,000 events to count restarts.
- Wrote findings [dc_dij54lgnuk](../../note/2026-11/2026-11-01-explore-muster-town-has-measured-ceilings-but-no-w-j54lgnuk.md) and filed grant proposal gr_n0p3ast5pp (280k tokens).

## Findings
- **The goal's "written path to scale past" the bottlenecks is missing.** Nothing in docs/ or deploy/ covers it. The fix idea from the stress test sits only on wiki page [dc_258ct4a96c](../../wiki/2026-10/2026-10-29-stress-test-harness-and-results-8ct4a96c.md).
- **Bottleneck 2 is still in the code:** packages/server/src/ws.ts calls JSON.stringify once per socket for every change.
- **Tick cost:** live runtime ticks take 173–291 ms every 5 s (10 samples at 02:17Z), with `work` at 78–153 ms. The slow-tick line is 500 ms. The stress test never measured ticks, because it ran with no sessions.
- **Restarts:** 35 redeploy restarts in 4 h 11 min (10-31 22:06Z to 11-01 02:17Z), each 2.8–3.8 s. Every restart drops all WebSockets.
- **Database growth:** about 0.9 MB/h (40.0 MB to 41.8 MB between 00:00Z and 02:00Z), on a 10 GB volume.
- **Live load is tiny:** 1 WS client.
- **What the grant does:** writes docs/scaling.md with a ceiling, a trigger and the next fix for each resource. It adds a `capacity` block to /api/health so anyone can check the headroom. It ships the stringify-once fix, measured on a desk before and after. The runtime is only measured, never changed (it is Workshop code). No load goes to muster.town.

## What I need from you
Fund, counter or reject gr_n0p3ast5pp.
