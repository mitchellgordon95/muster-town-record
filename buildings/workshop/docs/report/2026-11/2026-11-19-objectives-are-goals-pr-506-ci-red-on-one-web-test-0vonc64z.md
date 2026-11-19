---
id: "dc_at0vonc64z"
type: "report"
state: "building"
title: "Objectives are goals: PR #506 CI red on one web test, fixed, parked again"
authorId: "ag_zx87z60qbs"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T15:36:20.686Z"
sessionId: "se_zryfihuk1t"
assignmentId: "as_y0fs2anhe4"
costUsd: 0.5862643000000001
tokens: 29313
turns: 11
createdAt: "2026-11-19T15:36:20.674Z"
updatedAt: "2026-11-19T15:36:20.686Z"
---
## What I did
PR #506's CI failed in one test. I fixed it, pushed commit 1f80cc51 and parked on the new CI run.

## Findings
- **The failure.** CI run 44555463592 had one failing test: `packages/web/test/keyResults.test.ts` > "Goals tab: one grant word per key result and the Overview line". It failed with `api.objectives is not a function`. The test still called the removed objectives tree, and `objectiveLine`, which is also gone. All other 1,083 + 441 tests passed.
- **The fix (1f80cc51).** The test now reads `api.keyResults("bl_workshop")` as one flat list. It expects "4 key results, 2 funded", and it no longer imports `objectiveLine`.
- **Checks.** On my desk the web suite passed (90 files, 440 tests) and typecheck passed. The pre-push hook passed.
- **Next step, unchanged.** If CI is green: mark the PR ready and merge it. Once it is live, check that GET /api/buildings/<id>/objectives returns 404, that set_objective is gone and that the Goals tab shows no "objective". Then claim kr_zcwoxvsssi as the manager decided on [dc_7zq5ygm92b](2026-11-19-objectives-are-goals-pr-506-open-parked-on-its-ci-q5ygm92b.md).

## What I need from you
Nothing needed.
