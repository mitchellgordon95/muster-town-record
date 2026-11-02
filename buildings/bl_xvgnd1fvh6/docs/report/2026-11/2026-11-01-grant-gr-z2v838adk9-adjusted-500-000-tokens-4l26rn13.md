---
id: "dc_5c4l26rn13"
type: "report"
state: "building"
title: "Grant gr_z2v838adk9 adjusted: 500,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:89840:bl_xvgnd1fvh6"]
decision: "approve"
decisionNote: "Taken in: gr_z2v838adk9 adjusted to 500,000 (231,114 spent) and funded again. Its held step as_wp3cuxl7tx (PR #210 merge + live check) started by itself at 00:46:29Z; steps 2 (as_1rfpjhejek, recover.sh + README \"Recover\") and 3 (as_5tx4c007jx, timed drill) stay chained behind it. No new assignment needed."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T00:46:50.320Z"
createdAt: "2026-11-01T00:46:23.365Z"
updatedAt: "2026-11-01T00:46:50.320Z"
---
Written by the town: Mitchell adjusted grant gr_z2v838adk9 at its checkpoint (event 89840, 2026-11-01 00:46 UTC).

## Summary

Grant gr_z2v838adk9 "Make a dead muster.town volume a 30-minute, one-command recovery from the latest hourly copy, and stop a fresh empty town from overwriting or burying the good backups." adjusted by Mitchell: 500,000 tokens.

Status funded; 231,114 of 500,000 tokens spent; key results kr_7svvwv6lr5 [at-risk] If muster.town's Fly volume or host dies, the town is back with its state from the latest hourly copy within 30 min of a volume being created, with no hand-built tarball, and a fresh volume can never overwrite or bury the good backups.; kr_17cd844e42 [on-track] Empty-boot guard: a town with no backup history never overwrites or buries existing copies; kr_cc9dc81c96 [on-track] First-boot restore picks the newest good copy and skips a corrupt one; kr_36d053ac89 [not-started] Live unchanged after merge; kr_ccca476c37 [not-started] Timed recovery drill.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
