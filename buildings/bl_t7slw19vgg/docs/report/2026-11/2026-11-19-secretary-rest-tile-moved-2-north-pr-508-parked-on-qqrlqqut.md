---
id: "dc_a9qqrlqqut"
type: "report"
state: "building"
title: "Secretary rest tile moved 2 north: PR #508, parked on CI"
authorId: "ag_wrdhlx2rwo"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T15:33:15.876Z"
sessionId: "se_rns8zr6a63"
assignmentId: "as_h0yefv3mi1"
costUsd: 0.6769611000000003
tokens: 33848
turns: 18
createdAt: "2026-11-19T15:33:15.867Z"
updatedAt: "2026-11-19T15:33:15.876Z"
---
## What I did
- Moved the hydrant's `rest` from `{x:1,y:-1}` to `{x:1,y:-3}` in packages/core/src/world/furniture.ts. The Secretary's default tile goes from Town Hall lot (3,5) to (3,3), one tile east and three north of the hydrant, just under the library shelves. (3,2) is a shelf, so (3,3) is as far north as he can go in that column. The hydrant stays where it is.
- Updated packages/core/test/town-hall-rests.test.ts to pin the new tile, plus docs/architecture.md. Added the log entry docs/log.d/2026-11-19-teo-2-secretary-north.md.
- PR: https://github.com/mitchellgordon95/muster-town/pull/508 (draft).

## Findings
- (3,3) is floor and is not on a stand: the library stand is (4,3) and the manual stand is (7,3). So restBy() takes the tile itself rather than a fallback. The rest-tile test passes and checks that it is walkable, inside the hall and on no other place's tile.
- Typecheck is green. In `check --fast`, 336 of 337 tests passed. The one failure was a timing assertion (`maxGap < 100` ms) in export-import/backup tests. Those files pass when run alone (36/36), so it was load flakiness.
- **Live has no custom spot.** GET /api/town shows desk:ag_7tiwyqva83 named "Secretary's spot by the hydrant" at (71,9), which is the default. So the new default will show once the change is deployed.
- **Next session:** if PR #508 is green, mark it ready and squash-merge it (no redeploy). Park on the deploy, then confirm the Secretary's desk place on live sits at y = old−2, which is (71,7) if the hall hasn't moved. Then `tell` Mitchell one line saying where he stands.

## What I need from you
Nothing needed.
