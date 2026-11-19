---
id: "dc_85lcbwswxg"
type: "report"
state: "building"
title: "Body-only drag is live (46669b9d in eb4d790); live checks covered only the gates, not a real drag"
authorId: "ag_77ir3m4u86"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Gates verified live, behaviour covered by tests on main. The positive drag needs a human with building.manage; not worth a \"do\" ask. Mitchell will see it the first time he drags a resident."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-19T15:19:55.870Z"
sessionId: "se_x08rw1k80x"
assignmentId: "as_2mvdlp2nr9"
costUsd: 0.6904569
tokens: 34523
turns: 20
createdAt: "2026-11-19T15:19:40.566Z"
updatedAt: "2026-11-19T15:19:55.870Z"
---
## What I did
- Checked live /api/health: commit eb4d790 (started 2026-11-18 00:33Z). `git merge-base --is-ancestor 46669b9d eb4d790` succeeds, so PR #493 is live.
- Called POST /api/agents/:id/drop on live with every login I have.
- Ran the PR's tests on main.
- Rewrote the topic page [dc_kmrianpcp1](../../wiki/2026-11/2026-11-16-drag-residents-with-the-grasper-hand-rianpcp1.md).

## Findings
- **The live gates match the card.** Agent token → 403 "Only humans can move agents on the map." No token → 401. The test account (dungeonrpg99-ops, role:visitor only, never let in) → 403 "Ask for access first". No state changed.
- **I could not do a positive drag on live.** The core rule (ops.ts `dropAgent`) lets only humans with building.manage, or admins, drop an agent. No agent can do it, and the test account has neither role. So these are **unchecked on live**:
  - the body moves and the desk stays;
  - the rest spot sticks;
  - dropping on the desk clears the spot;
  - wall, water and doorway tiles are refused;
  - an admin can drag the Secretary.
- **The tests cover all of these and pass on main.**
  - packages/core/test/rest-spot.test.ts: 2/2. It covers refused walls, furniture, doors and off-map tiles; the desk staying put; walking home to the spot; the desk tile clearing the spot; and the Secretary.
  - packages/server/test/rest.test.ts, the drop case: the desk stays, the desk tile clears the spot, a wall gets 400, an agent token gets 403.
- The live /api/town has no custom "X's spot" place yet, only the Secretary's and Planner's defaults. Nobody has dropped a resident on live since the deploy.
- No browser drag: only a human with building.manage can do one, so all checks were API-only.
- Nothing differs from the card, so I did not tell Mitchell.

## What I need from you
Optional: a human with building.manage (e.g. Mitchell) drags one UI/UX resident onto the floor and reloads, to see the body move, the desk stay and the spot stick. No agent login can do that check.
