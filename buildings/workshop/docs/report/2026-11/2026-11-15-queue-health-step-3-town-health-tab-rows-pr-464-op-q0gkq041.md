---
id: "dc_gkq0gkq041"
type: "report"
state: "building"
title: "Queue health step 3: Town health tab rows, PR #464 open, parked on CI"
authorId: "ag_gbtt8dcddj"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T22:39:16.595Z"
sessionId: "se_xr3bdl7qwh"
assignmentId: "as_tk1cocz4er"
costUsd: 1.3644490999999999
tokens: 68222
turns: 26
createdAt: "2026-11-15T22:39:16.580Z"
updatedAt: "2026-11-15T22:39:16.595Z"
---
## What I did
Built the Town health tab section for grant gr_pdja05z2f1 step 3. Pushed it and opened draft PR #464 (https://github.com/mitchellgordon95/muster-town/pull/464). Rewrote topic page [dc_271txc8zem](../../wiki/2026-11/2026-11-12-queue-health-gr-pdja05z2f1-1txc8zem.md).

## Findings
- web `StatsPanel.tsx`: the Town health tab now also loads GET /api/health and passes its `legible` to `HealthView`.
  - "Queue health, last 14 days" sits above the token tiles. It always shows money, click and policy rows: minutes on card, and questions before deciding with the lines said. A type with no sample reads "none yet (no sample)". Credential, do and meeting rows appear when that type was decided. Then come gates per funded grant, grants at a gate today and budget used. Last is the line "Few gates with high budget use: work is running past review", red with role=alert when `gates.warning` is true.
  - "Queue and grants, last 14 days" shows every other legible measure as one plain-words row: open asks (per target, folds), oldest open ask, time to decide per type, retired before read, adjust asks per funded grant, closed grants that held, spent over size S/M/L, sessions per step, grants at a gate now, card rewrites, screen views.
  - Each row carries a `what` line. "What the numbers are" lists them all.
- `api.ts` `LegibleView` copies core `LegibleMeasures` by hand. A new core measure needs a field here and a row.
- Mock fixture `legible` is returned by the mock `health()`. The new render test in `statsPanel.test.tsx` checks the order, the rows, the warning crossed and not crossed, and a "what" line for every row. It passes (7/7). `npm run typecheck` is clean. The pre-push check passed.
- Live check not done yet: it needs the merge and the deploy.

## What I need from you
Nothing needed.
