---
id: "dc_mf6oelioq5"
type: "flag"
state: "building"
title: "ok actually let me just click and drag residents to new locations in the UI, if i want them somewhere else. like with a…"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag (dc_mf6oelioq5, planted at (76,9) in the UI / UX just now, after yesterday's \"move the hydrant\" flag): \"ok actually let me just click and drag residents to new locations in the UI, if i want them somewhere else. like with a little grasper hand\".\n\nShip it as one PR, merge on green, no redeploy (CI deploys main).\n\nWhat exists already (read before designing): \"Edit layout\" mode drags a room's furniture pieces with grab/grabbing cursors and a server dry run per change (web/src/map/layoutEdit.ts, web/src/map/MapCanvas.tsx:84-140, LayoutToolbar.tsx; server rules in core/src/world/furniture.ts, saved via world.ops.updateFurniture). A resident's standing spot is its desk: a desks row (n, agentId, buildingId) maps to the room's `desk:<n>` piece and its stand tile (core/src/world/layout.ts:152-179, furniture.ts:87; world.layout.deskOf / claimDesk). Residents walk back to their desk at the next session start (docs/architecture.md:144), so a drag that only sets `pos` would not stick.\n\nWhat to build: in the normal map view (not only in Edit layout), a human with building.manage (or admin) can mouse-down on a resident or visitor sprite and drag it; the cursor is a grasper hand (grab on hover, grabbing while dragging; a small pixel hand sprite over the dragged agent is welcome if cheap). On drop: (a) on another desk of the same building, free or occupied: the agent takes that desk slot (swap with the occupant if any), via a new small endpoint that rewrites the desks rows; (b) on a free floor tile of its own room: the agent's desk piece moves there, reusing the furniture rules (dry run; refuse with a toast on an invalid tile, the sprite snaps back); (c) anywhere else (another building, grass): snap back with a one-line toast saying why. The agent's body walks or teleports to the new stand tile at once so Mitchell sees the result without waiting for a session. Touch: long-press to grab is fine; skip if it costs more than an S. Keep Edit layout mode as is. Add a test for the endpoint and one for the drop rules. Say in the report what a human does to try it on the live town and what the three drop cases do."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-16T18:15:05.768Z"
flagPos: {"x":76,"y":9}
pickedUpAt: "2026-11-16T18:13:52.120Z"
pickedUpBy: "ag_s1kuuuo54b"
createdAt: "2026-11-16T18:13:33.764Z"
updatedAt: "2026-11-16T18:15:05.768Z"
---
ok actually let me just click and drag residents to new locations in the UI, if i want them somewhere else. like with a little grasper hand
