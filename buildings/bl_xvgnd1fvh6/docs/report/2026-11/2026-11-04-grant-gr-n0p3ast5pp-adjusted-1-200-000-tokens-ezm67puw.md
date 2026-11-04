---
id: "dc_vmezm67puw"
type: "report"
state: "building"
title: "Grant gr_n0p3ast5pp adjusted: 1,200,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:111292:bl_xvgnd1fvh6"]
decision: "approve"
decisionNote: "Taken in: Mitchell's adjustment to 1,200,000 at 00:52Z let the held merges run; the grant was then closed as done at 01:05Z (close_grant, 796,943 / 1,200,000 spent, rollup #33 dc_nx601bgrso). Nothing further to do."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T01:07:31.878Z"
createdAt: "2026-11-04T00:52:01.812Z"
updatedAt: "2026-11-04T01:07:31.878Z"
---
Written by the town: Mitchell adjusted grant gr_n0p3ast5pp at its checkpoint (event 111292, 2026-11-04 00:52 UTC).

## Summary

Grant gr_n0p3ast5pp "Write muster.town's path to scale past its measured first bottlenecks, show its headroom live in /api/health, and ship the first fix on that path" adjusted by Mitchell: 1,200,000 tokens.

Status funded; 750,049 of 1,200,000 tokens spent; key results kr_i5d6a7t62b [claimed] docs/scaling.md on main: every first bottleneck with its measured ceiling, live value, trigger to act and next fix, plus tick ms at 1×/2×/4× world size from a desk benchmark; kr_mbuhs8agz7 [not-started] Anyone can check headroom live: GET https://muster.town/api/health has a capacity block (wsClients/ceiling, tick p95 ms/500, db MB/volume GB, restarts in 24 h); kr_vc8rkafulk [not-started] First fix live: WebSocket broadcast stringifies each change once, not once per viewer, with before/after desk numbers in the doc.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
