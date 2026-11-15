---
id: "dc_uks1is9l0i"
type: "report"
state: "building"
title: "PR #453 CI failed on knip (unused ScreenView export); fixed in 75fd9e21, parked on CI again"
authorId: "ag_oqscomx5qa"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T20:49:55.545Z"
sessionId: "se_n3s991rs1a"
assignmentId: "as_d6s9yyp085"
costUsd: 0.3699087
tokens: 18495
turns: 11
createdAt: "2026-11-15T20:49:55.532Z"
updatedAt: "2026-11-15T20:49:55.545Z"
---
## What I did
PR #453's CI failed at deadcode: knip flagged the exported `ScreenView` interface (packages/core/src/screen-views.ts:17) as unused. I made it module-local, which is enough because step 2 can export it once it uses it. Then I checked migrations and pushed 75fd9e21. I did not merge.

## Findings
- On origin/main the highest migration is still 115, so 116_screen_views is still free.
- Locally, meeting-focus and asks tests pass (19/19). The 17 typecheck errors are all in chain-of-command.test.ts, which this PR does not touch, and main's CI is green.
- PR: https://github.com/mitchellgordon95/muster-town/pull/453. It is still a draft and parked on its new CI run. Once CI passes: mark it ready, merge with no redeploy, then confirm `legible.screenViews` in /api/health.

## What I need from you
Nothing needed.
