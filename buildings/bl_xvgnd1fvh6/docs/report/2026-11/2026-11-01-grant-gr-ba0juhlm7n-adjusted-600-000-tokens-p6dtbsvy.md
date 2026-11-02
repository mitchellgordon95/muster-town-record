---
id: "dc_dop6dtbsvy"
type: "report"
state: "building"
title: "Grant gr_ba0juhlm7n adjusted: 600,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:89876:bl_xvgnd1fvh6"]
decision: "approve"
decisionNote: "Taken in: gr_ba0juhlm7n adjusted to 600,000 (197,036 spent), funded again after Mitchell approved rollup #27 at 00:47Z. Its held step 2 (as_03g3ph6i35) was written before PR #227 moved the run into a worker and before as_fb264lb7m0 took the 01:00Z lag sample, so I replaced it with a fresh step 2 (restore drill from an hourly copy → README \"Drill\"; lag evidence reused from as_fb264lb7m0) that waits on that sample. Step 3 (sc_zyj6w0mygq daily 05:35Z from 11-02) unchanged."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T00:47:45.857Z"
createdAt: "2026-11-01T00:46:57.441Z"
updatedAt: "2026-11-01T00:47:45.857Z"
---
Written by the town: Mitchell adjusted grant gr_ba0juhlm7n at its checkpoint (event 89876, 2026-11-01 00:46 UTC).

## Summary

Grant gr_ba0juhlm7n "Cut muster.town's worst-case data loss from ~24 h to 1 h: hourly encrypted off-site copies of town.db, each one re-downloaded and checked" adjusted by Mitchell: 600,000 tokens.

Status funded; 197,036 of 600,000 tokens spent; key results kr_y7u2m9hk9y [on-track] muster.town loses at most 1 hour of town state if its Fly volume dies: an encrypted off-site copy of town.db lands every hour, and a restore from the latest hourly copy is proven; kr_bd08a0607a [claimed] Unit tests: hourly schedule, boot catch-up at > 1 h, tiered retention keeps 48 hourly + 30 daily and deletes the rest, verify step fails loudly on a corrupted object; kr_cee8c26801 [on-track] Live cadence: copies land every hour for a day; kr_1a69c0a3be [not-started] Live cost: the hourly run doesn't stall the server.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
