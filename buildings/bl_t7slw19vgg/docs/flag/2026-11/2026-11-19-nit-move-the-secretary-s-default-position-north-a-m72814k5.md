---
id: "dc_hrm72814k5"
type: "flag"
state: "building"
title: "nit: move the secretary's default position north a few tiles"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag (nit): move the Secretary's default position north a few tiles. Where it comes from: the Secretary rests by the hydrant (TOWN_HALL_RESTS in packages/core/src/world/layout.ts:22); the hydrant piece in packages/core/src/world/furniture.ts:75 sits at lot (2,6) with `rest: { x: 1, y: -1 }`, so the Secretary's default tile is lot (3,5), one tile north-east of the hydrant; restBy() in layout.ts:134-145 uses that tile when it is walkable and not a stand, door or other rest spot, else falls back to tiles around the stand. Do: move the default rest tile 2-3 tiles north (e.g. rest { x: 1, y: -3 } or { x: 1, y: -4 }, i.e. lot (3,3) or (3,2); the Town Hall is 17x11 with walls at y=0 and the board at (8,0), so stay inside the floor, y>=1, and check nothing else (board stand at (8,1), mod station, visitor bench) collides). Keep the hydrant itself where it is unless moving the rest tile alone looks wrong on the map. Update the rest-spot tests (packages/core/test/rest-spot.test.ts and any Town Hall layout test that pins the Secretary's tile), run `npm run check --fast`, open a small PR, merge it green (no redeploy; the server pulls prod itself), add a docs/log.d entry. Note: a human-dragged custom spot for the Secretary (PR #493) overrides the default; say in your report whether live has one (GET /api/town places, \"Secretary's spot\"). After the deploy, check on live that the Secretary idles on the new tile and tell Mitchell with a one-line `tell` where it now stands."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-19T15:20:38.607Z"
flagPos: {"x":70,"y":11}
pickedUpAt: "2026-11-19T15:20:03.606Z"
pickedUpBy: "ag_s1kuuuo54b"
createdAt: "2026-11-19T15:18:39.354Z"
updatedAt: "2026-11-19T15:20:38.607Z"
---
nit: move the secretary's default position north a few tiles
