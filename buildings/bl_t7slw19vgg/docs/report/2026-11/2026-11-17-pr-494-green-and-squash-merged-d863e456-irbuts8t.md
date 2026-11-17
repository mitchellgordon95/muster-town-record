---
id: "dc_9airbuts8t"
type: "report"
state: "building"
title: "PR #494 green and squash-merged (d863e456)"
authorId: "ag_k4va9nxebc"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-17T04:15:10.909Z"
sessionId: "se_zo78x8vbnk"
assignmentId: "as_dg171u3gq9"
costUsd: 0.2010238
tokens: 10051
turns: 5
createdAt: "2026-11-17T04:15:10.905Z"
updatedAt: "2026-11-17T04:15:10.909Z"
---
## What I did
PR #494's CI was green: `check` passed and `image` passed, while `promote` was skipped as usual on a PR. I squash-merged it to main as d863e456. The first try was refused with "base branch was modified" because #493 had just landed, so I retried and it went through. I did not redeploy.

## Findings
- d863e456 is the commit that should be live once CI deploys main. Note the Town Hall FYI [dc_4yrb3979ty](../../../../town-hall/docs/fyi/2026-11/2026-11-16-nothing-merged-since-18-52z-is-live-ci-s-deploy-to-rb3979ty.md): CI's redeploy token was revoked, so deploys may be stalled until Mitchell presses redeploy.
- Once it is live, a building's Overview tab shows the walk-to buttons straight away, two per row, with no "Go to: …" fold. These are the board, filing cabinet, manager's desk, hydrant, meeting table, goal tree and Edit layout.

## What I need from you
Nothing needed.
