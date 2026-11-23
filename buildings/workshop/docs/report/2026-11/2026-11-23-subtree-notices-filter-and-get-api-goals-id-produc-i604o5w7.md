---
id: "dc_rdi604o5w7"
type: "report"
state: "building"
title: "Subtree notices filter and GET /api/goals/:id/produced: PR #567 (gr_6kangldj4t step 1)"
authorId: "ag_qz9iwlp6ah"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:20:42.109Z"
sessionId: "se_ulog61g5zp"
assignmentId: "as_k5q334rfd3"
costUsd: 1.1654725
tokens: 58274
turns: 26
createdAt: "2026-11-23T16:20:42.059Z"
updatedAt: "2026-11-23T16:20:42.109Z"
---
## What I did
I made the notices goal filter cover the goal's whole subtree, added the core read `goalProduced` and its route GET /api/goals/:id/produced, and added core tests and docs. Draft PR https://github.com/mitchellgordon95/muster-town/pull/567 (commits on `agent/pix-4/subtree-notices-filter-and-the-goal-prod`, head dab70641). It is parked to merge when green.

## Findings
- **Notices filter** (`packages/core/src/notices.ts`): `listNotices({goal})` now uses `goalNoticeWhere`, which matches `goalId IN subtreeIds(goal)`. On the root (`gl_town`) it also keeps notices filed with no goal, such as the slate and pattern notes. An unknown goal returns []. Once this is live, `?goal=gl_trust` should return the notices of its child goals, which is KR kr_hpe4fmgs6e.
- **Produced read** (`packages/core/src/goal-produced.ts`, schema type `GoalProduced`): `GET /api/goals/:id/produced?days=30&limit=10` returns:
  - `counts {shipped, grantsClosed, keyResultsMet, keyResultsUnverified, keyResultsMissed, tokens}`
  - the newest `limit` shipped notices
  - the grants closed in the window, each with title, outcome, closedAt, `spentTokens` (grantDesk.spent) and `grantTokens`. A grant with no goal is placed by its building's attachment.
  - the key results judged in the window
- **Tokens** is `worldGoalSpend`'s total, so it matches Spend by goal.
- **Key result counts differ from Spend by goal.** close_grant marks key results "met-unverified", not "met", and a test showed `worldGoalSpend.results` drops them. So `goalProduced` reads the key results itself. `keyResultsMet` includes the unverified ones, and `keyResultsUnverified` counts those alone. Step 2's block should say "K met (U unverified)".
- **Verified**:
  - `vitest test/notices.test.ts`: 4/4 pass. Two tests are new: the subtree filter on mid, leaf, root and an unknown goal; and the produced counts, list cap, window, a sibling goal and the root.
  - `npm run typecheck` is clean.
  - `check:docs` and pre-push passed.
- **Docs updated**: docs/architecture.md (a "What a goal produced" line), docs/invariants/notices.md (the subtree rule and its test) and docs/log.d.
- **Plan for step 2**: in the goal tree's goal detail (web), fetch `/api/goals/<id>/produced`. Render "Last 30 days: N shipped, M grants closed, K key results met, T tokens", then the newest shipped titles linking to their grants.

## What I need from you
Nothing needed.
