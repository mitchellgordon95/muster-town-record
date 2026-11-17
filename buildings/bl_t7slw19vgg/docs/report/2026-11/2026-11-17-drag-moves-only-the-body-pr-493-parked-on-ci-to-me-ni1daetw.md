---
id: "dc_q8ni1daetw"
type: "report"
state: "building"
title: "Drag moves only the body: PR #493, parked on CI to merge"
authorId: "ag_bz9c81k932"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T04:07:06.587Z"
sessionId: "se_l4xksceqqp"
assignmentId: "as_x9vxu57xw6"
costUsd: 2.3715507999999996
tokens: 118578
turns: 47
createdAt: "2026-11-17T04:07:06.582Z"
updatedAt: "2026-11-17T04:07:06.587Z"
---
## What I did
I checked the building thread first. Mitchell has not answered Teo's ask, so I built body-only drag. It is one PR: https://github.com/mitchellgordon95/muster-town/pull/493. I filed no second ask and rewrote the topic page [dc_kmrianpcp1](../../wiki/2026-11/2026-11-16-drag-residents-with-the-grasper-hand-rianpcp1.md).

## Findings
- **How it works now.** A drop saves the tile in a new additive table, `rest_spots` (migration 123). The pure rule is in core `world/rest-spot.ts`. `computeLayout` points the agent's `desk:<agentId>` place at the saved spot. Every walk home already reads that place: session start, the idle tick, meeting end and a rebuild. So the agent comes back to the spot. The desk furniture never moves. `world/desk-drop.ts`, its test and `/desk-drop` are deleted. The new route is `POST /api/agents/:id/drop`.
- **What Mitchell does on live, once it is live.** He drags any resident with the grasper hand.
  - Drop on floor, grass, path or paving, inside or outside a building: only the body moves. The toast says "X will rest here". The agent walks back to that spot after sessions.
  - Drop on its own desk's tile: the saved spot is cleared. The toast says "X is back at their usual spot".
  - Drop on a wall, furniture, water, a doorway or off the map: the body snaps back with a one-line reason.
  - The Secretary and the Planner in the Town Hall can be dragged the same way (admin).
  - Human avatars can never be dragged.
- **Tests.** I added core `rest-spot.test.ts`: the rule, the desk staying put, walking home to the spot, clearing the spot, and the Secretary. I replaced the server `rest.test.ts` drop test and added a Secretary case to the web `residentDrag.test.ts`. `npm run check --fast` passed except one timing flake in server `backup.test.ts` (a 111 ms gap against a 100 ms limit). That file passed 27/27 when I ran it again alone.
- **Live.** This is not live yet. After the squash-merge, CI deploys main by itself. The merge commit will be named in the continuation's report. One caution: the town-wide FYI says CI's deploy token was revoked, and live is still at 7a886f88 although main is at 17fa38b8. So this may wait on that fix.

## What I need from you
Nothing needed.
