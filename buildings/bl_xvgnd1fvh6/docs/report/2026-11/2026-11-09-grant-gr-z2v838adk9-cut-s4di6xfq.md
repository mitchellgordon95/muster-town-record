---
id: "dc_f1s4di6xfq"
type: "report"
state: "building"
title: "Grant gr_z2v838adk9 cut"
authorId: "system"
authorKind: "user"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:141996:bl_xvgnd1fvh6"]
decision: "approve"
decisionNote: "Taken in: Mitchell cut gr_z2v838adk9 at its second checkpoint (665,893 / 500,000). Steps 1-2 stay live (guards, first-boot restore, recover.sh, throwaway mode); the timed drill never ran. Cancelled the held drill check as_z2lbfto2dn (lane grant on a closed grant). The drill request dc_6gnk7y16y1 stays open: it still covers gr_ba0juhlm7n's hourly-copy drill row. No new work assigned."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-09T22:32:01.185Z"
createdAt: "2026-11-09T22:31:33.726Z"
updatedAt: "2026-11-09T22:32:01.185Z"
---
Written by the town: Mitchell cut grant gr_z2v838adk9 at its checkpoint (event 141996, 2026-11-09 22:31 UTC).

## Summary

Grant gr_z2v838adk9 "Make a dead muster.town volume a 30-minute" cut by Mitchell.

Status closed; 665,893 of 500,000 tokens spent; key results kr_7svvwv6lr5 [at-risk] If muster.town's Fly volume or host dies, the town is back with its state from the latest hourly copy within 30 min of a volume being created, with no hand-built tarball, and a fresh volume can never overwrite or bury the good backups.; kr_17cd844e42 [claimed] Empty-boot guard: a town with no backup history never overwrites or buries existing copies; kr_cc9dc81c96 [claimed] First-boot restore picks the newest good copy and skips a corrupt one; kr_36d053ac89 [claimed] Live unchanged after merge; kr_ccca476c37 [not-started] Timed recovery drill.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
