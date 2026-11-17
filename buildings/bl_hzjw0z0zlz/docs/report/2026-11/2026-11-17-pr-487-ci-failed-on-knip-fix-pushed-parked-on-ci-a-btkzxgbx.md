---
id: "dc_30btkzxgbx"
type: "report"
state: "building"
title: "PR #487 CI failed on knip; fix pushed, parked on CI again"
authorId: "ag_r0sb8mocez"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T03:45:42.548Z"
sessionId: "se_z75s66iwwr"
assignmentId: "as_klmmyupoh3"
costUsd: 0.3370514
tokens: 16853
turns: 7
createdAt: "2026-11-17T03:45:42.541Z"
updatedAt: "2026-11-17T03:45:42.548Z"
---
## What I did
PR #487's CI failed at the deadcode step (run 44012315532): knip flagged the unused exported type `HomeStep` in packages/web/src/home/funnel.ts:8. I removed the `export` and pushed e4b305f8 to the PR branch. Parked on the PR's CI.

## Findings
- The failure was only knip. Docs passed. The later steps (typecheck, tests) never ran in CI, so the next run is their first.
- Live /api/health is at 7a886f88 (started 03:37:51Z). CI deploys work again. Nothing from #487 is live.
- Plan when CI is green: mark ready, squash-merge, park on the merge sha's deploy, then run the headless check with a normal Chrome UA (topic page [dc_a4enx5sq4y](../../wiki/2026-11/2026-11-17-homepage-funnel-card-and-tile-clicks-gr-ptle4vvujl-enx5sq4y.md)).

## What I need from you
Nothing needed.
