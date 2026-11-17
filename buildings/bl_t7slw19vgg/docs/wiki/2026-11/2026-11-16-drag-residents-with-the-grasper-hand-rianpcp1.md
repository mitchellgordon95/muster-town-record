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
updatedAt: "2026-11-17T04:06:55.706Z"
---
Flags [dc_mf6oelioq5](../../flag/2026-11/2026-11-16-ok-actually-let-me-just-click-and-drag-residents-t-6oelioq5.md) (first build, PR #477, 77c6073c: moved the desk) and [dc_d2wkuhoh1l](../../flag/2026-11/2026-11-17-the-drag-and-drop-residents-only-kind-of-works-why-wkuhoh1l.md) (Mitchell: "move just the character"). Now **body only**: PR #493 (open, parked on CI to squash-merge; not live yet).
- A drop saves the tile in table `rest_spots` (migration 123): relative to the building lot it is in, else absolute. Pure rule: packages/core/src/world/rest-spot.ts `restDrop` / `restTile`.
- Allowed: any walkable tile (floor, grass, path, paving), inside or outside buildings. Refused with a toast: wall, furniture, water, a doorway, off the map. Another agent's tile is allowed.
- Dropping on its own default tile (desk stand, or the Town Hall rest by hydrant / goal tree) deletes the row.
- computeLayout moves the `desk:<agentId>` place to the spot (named "X's spot"). Every walk home reads that place (home.ts walkHome, runtime walkToDesk, presence homeSpot), so the agent comes back there. The desk slot keeps the default (`WorldMap.defaultHomeOf`). If the spot stops being standable (furniture moved onto it), the default holds.
- Endpoint: POST /api/agents/:id/drop {x,y} → {pos, home}. Gate: building.manage on the agent's building, or admin. The Secretary and the Planner are draggable by an admin. Human avatars never. /desk-drop and world/desk-drop.ts are gone. Edit layout is the only way to move furniture.
- Not built: touch long-press (mouse only).
