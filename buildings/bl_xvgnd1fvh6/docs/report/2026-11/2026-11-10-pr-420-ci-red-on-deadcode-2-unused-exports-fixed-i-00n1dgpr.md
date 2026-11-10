---
id: "dc_y300n1dgpr"
type: "report"
state: "building"
title: "PR #420 CI red on deadcode (2 unused exports): fixed in 4c19649, parked on CI"
authorId: "ag_cokys9mdjk"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Deadcode fix 4c19649 pushed to PR #420; continuation as_wc50my2rc5 already waits on its CI to mark ready and merge. Nothing more to queue."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-10T21:17:00.803Z"
sessionId: "se_uclrj9ij98"
assignmentId: "as_lvu0lixdz1"
costUsd: 0.429884
tokens: 21494
turns: 12
createdAt: "2026-11-10T21:16:53.879Z"
updatedAt: "2026-11-10T21:17:00.803Z"
---
## What I did
PR #420's CI failed at the `deadcode` check after 20 s. It flagged two unused exports: `CHANGES_FORMAT` (packages/runtime/src/redeploy.ts:163) and `RedeployChangeLink` (packages/web/src/redeploy.ts:84). I removed `export` from both and pushed 4c196499 to the PR branch.

## Findings
- Desk checks: `deadcode` and `typecheck` pass. Runtime tests pass (250/250). Web tests pass (368/368).
- The full local `npm run check` failed at tests. The web suite reports 4 unhandled errors because `happy-dom` is missing from my desk's node_modules. That is a desk install gap, not caused by this PR. CI is the real check.
- Next: once CI is green, mark #420 ready and merge it. CI then deploys it, with no `redeploy` call. After that, check that the next deploy's HUD card lists its changes (`payload.run.changes`). If CI is red, fix it.

## What I need from you
Nothing needed.
