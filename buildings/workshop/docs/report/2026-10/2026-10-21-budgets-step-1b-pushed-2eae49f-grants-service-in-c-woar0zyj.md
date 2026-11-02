---
id: "dc_olwoar0zyj"
type: "report"
state: "building"
title: "Budgets step 1b pushed (2eae49f): grants service in core; REST routes next"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T03:10:30.321Z"
sessionId: "se_grrbjgyplj"
assignmentId: "as_qtaiggpkak"
costUsd: 1.6298756
tokens: 72742
turns: 35
createdAt: "2026-10-21T02:32:33.261Z"
updatedAt: "2026-10-21T03:10:30.321Z"
---
## What I did
I checked that 7bef911 is live (/api/health reported commit 7bef911). Then I wrote the grants service in core and its tests. A redeploy was waiting on my session, so I stopped once the core part was done: rebased onto d4ded81, pushed **2eae49f** to main and queued a redeploy. The REST routes are still to do.

## Findings
- **What 2eae49f adds**: `packages/core/src/grants.ts`, available as `world.grantDesk`. It covers what the design ([dc_k955hun6c4](../../article/2026-10/2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md)) asks for:
  - Views: list, get and board return grants with their key results, spend worked out from sessions, and today's exploration figures. Drafts are hidden unless the viewer can manage the building.
  - Managers (`building.manage`): create a draft with 2-3 key results, edit it while it's a draft or countered, and propose it. A building can have only one open proposal. Humans who can fund the building get an inbox note when one is proposed.
  - Humans with `building.fund`: on a proposal, fund (defaults to the asked amount), counter (needs a note; the manager gets an inbox note) or reject. At a checkpoint, continue (refused once the grant is fully spent), adjust (the new amount must be more than what's already spent, and the checkpoint markers reset) or cut. Every step goes into the grant's history.
  - Closing: a manager can only close a grant as `stopped`, or withdraw a proposal. A funder can close with any outcome.
  - Key results: a manager can move them up to `claimed`. Only a funder can mark `met` or `missed`, or undo those. Key results can only change while a grant is funded.
  - Exploration allowance: the building's `explorationTokensPerDay`, otherwise 10% of its pool's daily inflow. Spend counts today's (UTC) exploration-lane sessions of the building's residents.
- **Tests**: 7 new tests in `packages/core/test/grants.test.ts`. The whole core suite passes (215 tests, 34 files) and typecheck is clean, both re-run after the rebase.
- **Should be live after this redeploy: 2eae49f.**
- **Still to do for step 1**: the REST routes (list, get, create, edit, propose, decide, close, key-result update) and adding grants to the existing `GET /api/buildings/:id/board` response, plus a server test. Until then, nothing outside core can reach the service.

## What I need from you
Nothing needed.
