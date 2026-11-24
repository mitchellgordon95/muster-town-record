---
id: "dc_8gvrrnfqkj"
type: "wiki"
state: "building"
title: "Town Hall interior: three lead pieces (mt_8imtwy68zc)"
authorId: "ag_axjvya6byd"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-24T22:07:42.636Z"
updatedAt: "2026-11-24T22:31:10.942Z"
---
Mitchell, 1:1 mt_8imtwy68zc (2026-11-24): the hydrant, the goal tree planner and the meeting desk are the three main things in the Town Hall. The town organization board goes outside. The library becomes tiny.

**Live.** PR #593 merged as 60d1bfd5 (2026-11-24 22:13:33Z); /api/health commit c47d6167 contains it. Duplicate PR #594 (Teo 2) is closed unmerged.

**Layout (lot-relative, 17x11, door at (8,10)):**
- Goal tree: 3-tile wall chart at (7..9, 0) over the door aisle, used from (8,1). `drawGoalChartTile` in sprites.ts. Planner rests at (9,1).
- Hydrant at (5,5), used from (5,6). Secretary rests at (6,2): seen live, not covering the hydrant.
- Meeting table at (10..13, 5), used from (11,6).
- Library 2 shelves (1..2,1); manual lectern (3,1). FYI board on the wall (13,0). Stats (15,3), schedule (15,6). Mod station (1..3,8), help sign (6,9), bench (10..11,9), planning desk (13..14,9).
- Town map = 1-tile `TILE.TOWN_MAP` board in the square, 3 tiles right of the hall door, mirroring the bulletin board 3 tiles left. Place `town-map`, buildingId null. Seen live: clicking it walks there and opens "The town map" planning panel (shape: Town square / Plain tree / Radial).

**Help card order:** PR #597 (as_g4jfu8no63) makes the hall's help card and map tour list hydrant, goal tree, meeting table first (hotspots 1-3), ported from #594. Live once it merges and /api/health contains it.

**Screenshots:** live hall + square + town map panel mf_k9eotp67f2 (2026-11-24). Earlier mock shots mf_rn86gy8z7s, mf_qv8a5sfrc5. Live screenshot script: ~/shots/live/s.mjs on Teo 1's desk (opens /workshop/, clicks the minimap at the hall, optional click on a map point).
