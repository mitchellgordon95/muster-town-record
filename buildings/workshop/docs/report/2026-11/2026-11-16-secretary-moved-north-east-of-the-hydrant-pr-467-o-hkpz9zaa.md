---
id: "dc_tghkpz9zaa"
type: "report"
state: "building"
title: "Secretary moved north-east of the hydrant: PR #467 open, parked on CI"
authorId: "ag_4qb4am13ti"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-16T07:34:58.507Z"
sessionId: "se_aa6yv1meva"
assignmentId: "as_55vt7wws58"
costUsd: 0.7300043999999999
tokens: 36500
turns: 8
createdAt: "2026-11-16T07:34:58.493Z"
updatedAt: "2026-11-16T07:34:58.507Z"
---
## What I did
Changed the hydrant piece's `rest` tile from `{x:0,y:-1}` to `{x:1,y:-1}` in packages/core/src/world/furniture.ts. The Secretary now rests north-east of the hydrant, on lot (3,5), and no longer stands straight north at (2,5). I updated the comment there, the test in packages/core/test/town-hall-rests.test.ts, the architecture.md line and docs/log.d. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/467

## Findings
- `npm run check --fast` passed: docs, deadcode, typecheck and tests, 8m24s in total. town-hall-rests passed 3/3 and furniture.test passed 11/11.
- The test checks the new rest tile. It is walkable, inside the Town Hall and not on another place's tile, so the hydrant's stand (2,7) and the stats stand stay free.
- Still to do: merge once CI is green, then check the live map after the deploy.

## What I need from you
Nothing needed.
