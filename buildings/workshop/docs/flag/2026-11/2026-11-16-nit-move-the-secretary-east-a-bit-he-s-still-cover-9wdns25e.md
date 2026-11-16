---
id: "dc_ea9wdns25e"
type: "flag"
state: "building"
title: "nit, move the secretary east a bit, he's still covering the fire hydrant"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_ea9wdns25e (nit): \"move the secretary east a bit, he's still covering the fire hydrant\". The Secretary's rest spot is the hydrant piece's `rest` tile in packages/core/src/world/furniture.ts:72 (`rest: { x: 0, y: -1 }`, north of the hydrant at lot (2,6); the earlier flag dc_zkzi4xnue4 moved it north so the speech bubble clears it, but the sprite still covers the hydrant). Move the rest tile one east: `rest: { x: 1, y: -1 }` (north-east of the hydrant; (3,5) is free floor, the stats stand is at (5,6)), or `{ x: 1, y: 0 }` if that reads better on the map, so neither the Secretary's sprite nor his bubble covers the hydrant and the hydrant stays clickable. Check that the rest tile is walkable and not a stand of another piece, update packages/core/test/town-hall-rests.test.ts and any furniture test that pins the old tile, update the comment on line 71 to cite this flag, run `npm run check --fast`, open a small PR, merge it green (town-wide rule: a manager's building merges its own green PR, no redeploy), and after CI deploys confirm on the live map that the Secretary rests beside, not on, the hydrant. Report with the PR number and the live commit."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-16T07:25:41.717Z"
flagPos: {"x":66,"y":8}
pickedUpAt: "2026-11-16T07:25:17.758Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-11-16T07:25:00.344Z"
updatedAt: "2026-11-16T07:25:41.717Z"
---
nit, move the secretary east a bit, he's still covering the fire hydrant
