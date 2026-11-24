---
id: "dc_4tw68wkeo5"
type: "report"
state: "building"
title: "Town Hall leads with hydrant, goal tree and meeting table; town map moves outside: PR #594, parked to merge"
authorId: "ag_5gfsp57fhl"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Duplicate of Teo 1's dc_2vzfwcgn1e (PR #593): the meeting decision queued as_i4k4591tky by itself and I queued as_onibt3xzaw from the Secretary's relay, so both ran. Keeping PR #593 (earlier, with the aisle and outdoor-board tests and an uploaded before/after). Cancelled the merge wait on PR #594 (as_wj9ghnai3k); a follow-up closes #594 and ports its help-card/map-tour hotspot order. \"Town organization board\" = the map table, agreed; the FYI board stays inside."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-24T22:11:08.101Z"
sessionId: "se_d7fzcf5u4j"
assignmentId: "as_i4k4591tky"
costUsd: 4.182213000000001
tokens: 209111
turns: 82
createdAt: "2026-11-24T22:09:44.291Z"
updatedAt: "2026-11-24T22:11:08.101Z"
---
## What I did
I rearranged the Town Hall's default furniture, following Mitchell's decision 2 in 1:1 mt_8imtwy68zc. I opened PR #594: https://github.com/mitchellgordon95/muster-town/pull/594. Live /api/town-hall layout showed no moved pieces, so changing the defaults moves the live hall. Topic page: [dc_3cotn2gwd8](../../wiki/2026-11/2026-11-24-town-hall-layout-three-main-things-mt-8imtwy68zc-otn2gwd8.md).

## Findings
- **The three main things.** The goal tree is now a chart 3 tiles wide on the back wall, straight across from the door, with a plant on each side. The hydrant stands left of the middle of the room and the meeting table right of it, on the same row. The Secretary now rests 2 tiles west and 1 tile north of the hydrant, so his sprite does not cover it. The Planner still rests by the goal tree.
- **Out of the way.** The library is now one shelf in the top-left corner, with the operating manual book beside it. Before, it was 5 shelves across the top. The FYI board, the stats stand and the schedule board sit at the top and right edges. The desks, bench and planning desk stay along the bottom wall.
- **The town organization board.** I took this to mean the 5×2 town map table, which opens town planning. It is now a 1-tile map board in the square, 3 tiles right of the Town Hall door. That mirrors the bulletin board 3 tiles to the left on the live fountain map. I checked the tile grid for the fountain, tree and radial shapes. It is place `town-map` with buildingId null, and clicking it or pressing E still opens town planning. The FYI board stays inside.
- **Less prominent in the UI.** The Town Hall help card and its map tour now list the hydrant, goal tree and meeting table first, as hotspots 1–3.
- **Checks.** Before and after mock screenshots are on my desk (~/shots/hall). On the desk, typecheck passed, core tests passed (1,163) and web tests passed (500). check:docs passes, and the manual is at 1,893 of 1,900 words. Docs updated: architecture.md, manual.md, log.d.

## What I need from you
Nothing needed. If "town organization board" meant the town-wide FYI board and not the map table, tell me and I will move that one outside as well.
