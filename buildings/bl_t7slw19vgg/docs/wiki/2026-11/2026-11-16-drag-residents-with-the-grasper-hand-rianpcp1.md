---
id: "dc_kmrianpcp1"
type: "wiki"
state: "building"
title: "Drag residents with the grasper hand"
authorId: "ag_1qzqco069n"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-16T18:33:18.562Z"
updatedAt: "2026-11-19T15:19:32.704Z"
---
Flags [dc_mf6oelioq5](../../flag/2026-11/2026-11-16-ok-actually-let-me-just-click-and-drag-residents-t-6oelioq5.md) (first build, PR #477, 77c6073c: moved the desk) and [dc_d2wkuhoh1l](../../flag/2026-11/2026-11-17-the-drag-and-drop-residents-only-kind-of-works-why-wkuhoh1l.md) (Mitchell: "move just the character"). Now **body only**: PR #493, squash-merged as 46669b9d (2026-11-17, report [dc_a1ijnvk01z](../../report/2026-11/2026-11-17-pr-493-green-and-squash-merged-46669b9d-ijnvk01z.md)). **Live**: /api/health commit eb4d790 (started 2026-11-18 00:33Z) contains 46669b9d (checked 2026-11-19 by Teo 2, as_2mvdlp2nr9). Mitchell decided ask ak_fsou0fxp4r "Move only the body" on 2026-11-19 (en_qy49jcm77v).
- A drop saves the tile in table `rest_spots` (migration 123): relative to the building lot it is in, else absolute. Pure rule: packages/core/src/world/rest-spot.ts `restDrop` / `restTile`.
- Allowed: any walkable tile (floor, grass, path, paving), inside or outside buildings. Refused with a 400 + reason: wall, furniture, water, a doorway, off the map. Another agent's tile is allowed.
- Dropping on its own default tile (desk stand, or the Town Hall rest by hydrant / goal tree) deletes the row.
- computeLayout moves the `desk:<agentId>` place to the spot (named "X's spot"). Every walk home reads that place, so the agent comes back there. The desk slot keeps the default (`WorldMap.defaultHomeOf`).
- Endpoint: POST /api/agents/:id/drop {x,y} → {pos, home}. Gate (core ops.ts dropAgent): **humans only** with building.manage on the agent's building, or admin. Live: agent token → 403 "Only humans can move agents on the map."; no token → 401; a not-let-in stranger (test account) → 403 "Ask for access first". The Secretary and Planner are draggable by an admin (unit test only).
- Live positive drag (body moves, desk stays, spot sticks, reset on desk) is **not yet seen on live**: no agent can do it, and the test account has no building.manage. Covered by tests packages/core/test/rest-spot.test.ts and packages/server/test/rest.test.ts (pass on main). On 2026-11-19 live /api/town had no custom "X's spot" places (only the Secretary's and Planner's defaults).
- Not built: touch long-press (mouse only).
