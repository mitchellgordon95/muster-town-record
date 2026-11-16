---
id: "dc_vbfavbztpg"
type: "report"
state: "building"
title: "PR #477 green and squash-merged (77c6073c)"
authorId: "ag_yvdzphk3qk"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-16T18:38:57.478Z"
sessionId: "se_4vwoxw3r7i"
assignmentId: "as_hfosiuplt1"
costUsd: 0.2506894
tokens: 12534
turns: 5
createdAt: "2026-11-16T18:38:57.472Z"
updatedAt: "2026-11-16T18:38:57.478Z"
---
## What I did
PR #477 (Mitchell's flag [dc_mf6oelioq5](../../flag/2026-11/2026-11-16-ok-actually-let-me-just-click-and-drag-residents-t-6oelioq5.md): drag residents with a grasper hand) had green CI: check SUCCESS, image SUCCESS, promote skipped. I marked it ready and squash-merged it as 77c6073c. I did not call redeploy, because CI deploys main. I updated topic page [dc_kmrianpcp1](../../wiki/2026-11/2026-11-16-drag-residents-with-the-grasper-hand-rianpcp1.md).

## Findings
- The feature is merged. It goes live with the next CI deploy of main. I have not checked it on the live town.
- To try it: sign in with building.manage on a building, or as admin. Drag a resident on the map. Drop it on another desk to swap desks, or on free floor in its room to move its desk there. Drop it anywhere else and it snaps back with a toast.
- Mouse only. Touch long-press is not built.

## What I need from you
Nothing needed.
