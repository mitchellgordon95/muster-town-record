---
id: "dc_zkzi4xnue4"
type: "flag"
state: "building"
title: "nit: move the secretary north of the fire hydrant, his speech bubble is blocking it"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_zkzi4xnue4 (nit): \"move the secretary north of the fire hydrant, his speech bubble is blocking it\".\n\nWhere it is in the code: packages/core/src/world/layout.ts:122-150. In the Town Hall, a resident in `rests` (the Secretary rests by the hydrant, the Planner by the goal tree) gets its desk at the first walkable tile right, left, below or above the piece's STAND (`restBy`, lines 128-137, order [1,0], [-1,0], [0,1], [0,-1]). The hydrant's stand is the tile below the hydrant (packages/web/test/hydrant.test.tsx:15 \"used from below\"), so the Secretary ends up right of the stand, and his speech bubble (drawn above his head by the web renderer) covers the hydrant sprite.\n\nDo: put the Secretary's rest spot NORTH of the hydrant tile itself (the tile above the hydrant's furniture cell, not above its stand), so the bubble rises above the hydrant and the hydrant stays visible. Smallest change that does it: let a rest piece say where its rest spot goes (e.g. the hydrant piece prefers the tile above its cell; fall back to the current right/left/below/above search when that tile is not walkable or is another stand). Keep the Planner's spot as it is unless the same rule improves it. The spot must stay walkable, inside the Town Hall, on no other place's tile, and the stream dots in packages/web/src/map/renderer.ts:562-580 (they settle at the Secretary's desk) must still look right. Update packages/core/test/town-hall-rests.test.ts (the Manhattan-distance-1 assertion against the stand will change: assert against the hydrant cell instead) and docs/log.d/<date>-<branch>.md. Open a PR, merge it green (no redeploy), and once /api/health shows the merge sha look at the live map: the Secretary should stand above the hydrant with the hydrant unobscured. Report with a screenshot if you can get one."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-15T22:00:53.866Z"
flagPos: {"x":69,"y":10}
pickedUpAt: "2026-11-15T22:00:20.588Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-11-15T22:00:01.425Z"
updatedAt: "2026-11-15T22:00:53.866Z"
---
nit: move the secretary north of the fire hydrant, his speech bubble is blocking it
