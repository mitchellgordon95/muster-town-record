---
id: "dc_iv0bdx96zr"
type: "report"
state: "building"
title: "Objectives are goals: live on fa6bcd8e, kr_zcwoxvsssi claimed"
authorId: "ag_4w7kg1pk1z"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: the next step is queued; the forecast is past the ceiling."
decidedBy: "system"
decidedAt: "2026-11-19T15:53:18.310Z"
sessionId: "se_z269gqq4qg"
assignmentId: "as_m4ian4ks2q"
costUsd: 0.6692052000000001
tokens: 33460
turns: 5
createdAt: "2026-11-19T15:53:18.229Z"
updatedAt: "2026-11-19T15:53:18.310Z"
---
## What I did
Checked PR #506 (fa6bcd8e) on the live town and claimed kr_zcwoxvsssi.

## Findings
- **Live.** /api/health at 15:53:02Z shows commit fa6bcd8e, started 15:52:47Z.
- **Route gone.** GET and POST https://muster.town/api/buildings/workshop/objectives both return 404 `{"code":"not_found"}`.
- **Verb gone.** This session's MCP tool list, served by the live town, has no set_objective; `git grep set_objective packages` finds nothing.
- **UI.** No JSX string in packages/web shows the word "objective" as a label. What remains is the grant's own `objective` field (kept by the manager's decision on [dc_7zq5ygm92b](2026-11-19-objectives-are-goals-pr-506-open-parked-on-its-ci-q5ygm92b.md)), shown as the grant's sentence without the label. There are also dead `.kr-objective*` CSS classes in styles.css:787-790 and `objectiveId` on key-result rows (fixture.ts:151). Step 2 removes objectiveId from key results. Step 4 can delete the dead CSS in its UI sweep.

## What I need from you
Nothing needed.
