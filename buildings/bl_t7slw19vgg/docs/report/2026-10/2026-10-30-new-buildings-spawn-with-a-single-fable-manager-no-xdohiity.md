---
id: "dc_irxdohiity"
type: "report"
state: "building"
title: "New buildings spawn with a single Fable manager, no residents (merged 90e0f82)"
authorId: "ag_jv2f2uty9s"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: PR #105 merged at 90e0f82. Starter building = one Fable manager."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-30T00:08:38.453Z"
sessionId: "se_i3qk52zord"
assignmentId: "as_5zqmmq86cw"
costUsd: 0.6556308000000002
tokens: 32782
turns: 27
createdAt: "2026-10-30T00:08:17.484Z"
updatedAt: "2026-10-30T00:08:38.453Z"
---
## What I did
I found the earlier fork's pushed branch (`agent/teo-2/new-buildings-spawn-with-a-single-manage`, commit bdfcea4) and reviewed it. The change was complete. I ran the checks to completion and merged origin/main twice (one conflict in docs/log.md, which I resolved). Then I merged PR https://github.com/mitchellgordon95/muster-town/pull/105 and queued a redeploy.

## Findings
- **What changed:** `packages/core/src/entities.ts` `seedStarterResidents` now creates exactly one town-named agent with model `claude-fable-5-1` (`STARTER_MANAGER_MODEL`, exported) and sets it as the building's manager. Before, it created 3 residents. This applies to both POST /api/buildings and a building drawn on the town plan. Existing buildings are untouched. No migration or web change was needed: the create form never had a residents-count field.
- **Checks:**
  - Typecheck passes.
  - Core suite: 478 of 479 tests passed. The one failure was a 5 s timeout in `wakes-step5.test.ts`, unrelated to this change; that file passes when run on its own, along with `starter-residents.test.ts`.
  - Server `rest.test.ts`: 21/21 passed.
- **Commit that should be live:** 90e0f82 (redeploy queued, not yet verified live).
- Topic page: [dc_2yk4xvbjym](../../wiki/2026-10/2026-10-30-new-building-starter-agents-k4xvbjym.md).

## What I need from you
Nothing needed.
