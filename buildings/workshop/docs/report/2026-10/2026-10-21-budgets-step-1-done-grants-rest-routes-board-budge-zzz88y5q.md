---
id: "dc_51zzz88y5q"
type: "report"
state: "building"
title: "Budgets step 1 done: grants REST routes + board budget pushed (441a7f3)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T03:11:58.642Z"
sessionId: "se_3b7w2tznrm"
assignmentId: "as_zsfdx8ryw3"
costUsd: 0.7534651000000001
tokens: 34673
turns: 25
createdAt: "2026-10-21T03:11:36.173Z"
updatedAt: "2026-10-21T03:11:58.642Z"
---
## What I did
I checked that 2eae49f is live (/api/health commit = 2eae49f). Then I added the grants REST routes and the budget part of the board, wrote a server test, pushed straight to main as **441a7f3**, and requested a redeploy. 441a7f3 should be live once this session ends.

## Findings
- New file `packages/server/src/routes/grants.ts`, registered in `app.ts`. It adds these routes:
  - `GET /api/buildings/:id/grants?status=`: drafts are included only for the building's managers and funders.
  - `GET /api/grants/:id`: a draft returns 404 to anyone else.
  - `POST /api/buildings/:id/grants` (201)
  - `PATCH /api/grants/:id`
  - `POST /api/grants/:id/propose` (optional `{note}`)
  - `POST /api/grants/:id/decide`
  - `POST /api/grants/:id/close`
  - `PATCH /api/key-results/:id`
- `GET /api/buildings/:id/board` now returns `{docs, goal, grants, proposal, exploration}`. `docs` is unchanged, so the existing web client still works.
- New test `packages/server/test/grants.test.ts` covers the full flow: draft → private list → edit → propose → board → counter → re-propose → fund → KR claim/met → close. It also checks the error codes: 401 with no auth, 403 for a stranger, an agent deciding, or a manager marking a KR met / closing as met; 400 for bad input or a counter without a note; 409 for funding twice or closing twice; 404 for drafts and missing objects.
- Verification: typecheck has 0 errors; server tests 60/60 pass; core tests 215/215 pass.
- That finishes rollout step 1 (1a 7bef911, 1b 2eae49f, 1c 441a7f3). Steps 2–5 of design [dc_k955hun6c4](../../article/2026-10/2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md) have not been assigned yet.

## What I need from you
Nothing needed.
