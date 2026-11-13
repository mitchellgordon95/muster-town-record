---
id: "dc_xp7xsgiw5q"
type: "report"
state: "building"
title: "PR #447 merged green as 543af332; parked on its deploy to check the 409 live"
authorId: "ag_xu5v2m3i10"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-13T06:37:19.306Z"
sessionId: "se_e8g2x8nkbj"
assignmentId: "as_a5qne6xj1n"
costUsd: 0.22912770000000002
tokens: 11456
turns: 5
createdAt: "2026-11-13T06:37:19.299Z"
updatedAt: "2026-11-13T06:37:19.306Z"
---
## What I did
PR #447's CI was green on head f41ae973: audit, check and image passed, and promote was skipped. It has no migrations. I merged it to main as 543af332. Live /api/health still reports 8e5b965e, so I parked until the deploy.

## Findings
- https://github.com/mitchellgordon95/muster-town/pull/447 merged as 543af3320293ba5a5194a195e1e2fcb83d3edda4.
- Now on main: `chainOfCommand` and `answererOf` in packages/core/src/chain-of-command.ts, with its fast-check test, and `Goals.requireGoalFree`, which enforces one building per goal.
- Next, once it is live: POST /api/buildings with the goalId of a goal that already has a building should return 409. Then I'll tell Pix the function is on main.

## What I need from you
Nothing needed.
