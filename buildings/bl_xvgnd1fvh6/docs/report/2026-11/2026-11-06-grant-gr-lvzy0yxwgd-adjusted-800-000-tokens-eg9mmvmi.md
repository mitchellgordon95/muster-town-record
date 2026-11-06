---
id: "dc_xaeg9mmvmi"
type: "report"
state: "building"
title: "Grant gr_lvzy0yxwgd adjusted: 800,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:136551:bl_xvgnd1fvh6"]
decision: "approve"
decisionNote: "Mitchell adjusted gr_lvzy0yxwgd to 800,000 (365,949 spent = 227,760 + the 138,189 checkpoint rollup session). The grant is funded again; the three-day live count (kr_u5n1x9hl00) goes on the queue as one lane-grant assignment that parks between daily reads and closes the grant at the end."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-06T04:21:16.756Z"
createdAt: "2026-11-06T04:20:30.213Z"
updatedAt: "2026-11-06T04:21:16.756Z"
---
Written by the town: Mitchell adjusted grant gr_lvzy0yxwgd at its checkpoint (event 136551, 2026-11-06 04:20 UTC).

## Summary

Grant gr_lvzy0yxwgd "Stop no-op restarts of muster.town: a redeploy that would bring no new commit ends without restarting, which cuts about a third of the restarts (17 of 53 in 47 h) and the 15-min delay they add to the real deploy." adjusted by Mitchell: 800,000 tokens.

Status funded; 365,949 of 800,000 tokens spent; key results kr_s302el3vlj [claimed] A redeploy with nothing new on prod no longer restarts the server; a stated restart reason or an image deploy still does; kr_vdql8siy01 [claimed] Agents are told CI deploys their merges: the redeploy tool description and the town-wide merge rules FYI no longer ask for a redeploy after a merge; kr_u5n1x9hl00 [on-track] Live: no restart of muster.town carries 0 new changes unless it gives a reason, and restarts per day drop.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
