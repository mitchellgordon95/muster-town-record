---
id: "dc_e7lildtrga"
type: "report"
state: "building"
title: "Bank pool and exploration budget now live on the goal, inherited down the tree (PR #160, eadf7de, redeploy queued)"
authorId: "ag_1a8j9p3s0n"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_n25udpflus","dc_rke20gvrqr"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/160"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: PR #160 eadf7de moves Bank pool + exploration budget onto goals (decision 3 of mt_n25udpflus, Mitchell's yes on the Bank). Live check queued separately. Rollup 34 Shipped item with mf_ef1cqsit5i; the permission change (exploration/day now needs goals.edit on the goal) goes in its \"Your call\"."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T05:55:10.332Z"
sessionId: "se_7g24piogwg"
assignmentId: "as_u2v8yvo2w1"
costUsd: 5.643023200000002
tokens: 282151
turns: 98
createdAt: "2026-10-31T05:54:57.982Z"
updatedAt: "2026-10-31T05:55:10.332Z"
---
## What I did
Mitchell now sets a building's **Bank pool** and **exploration budget** on the goal it is attached to, not on the building. Open the goal tree, pick a goal, and use the new **Funding** block under the owner line. Admins get a pool dropdown. Anyone who can edit that goal (an admin or the goal's owner, never an agent) can set **Exploration / day**. A goal that sets neither inherits the nearest value from a goal above it; when no goal up the tree sets one, the pool is General and the allowance is the default (10% of the pool's daily inflow). The building's Settings no longer have the Bank pool or Exploration budget sections. Its Overview shows "Pool: X (from goal Y)". The Bank's Pools tab lists which goals, and so which buildings, each pool funds.

This is a Bank change. It went ahead because Mitchell agreed to it in decision 3 of 1:1 mt_n25udpflus, which names the pool explicitly.

What the back-fill moves, based on the live data I read at ~05:20Z (it runs when eadf7de boots):

| Goal | From building | poolId | Exploration / day |
|---|---|---|---|
| gl_join (Steer) | Town Workshop | general | none (default stays) |
| gl_bl_hzjw0z0zlz | Onboarding | general | none |
| gl_bl_xvgnd1fvh6 | Prod | general | none |

Bank Transparency, Code Legibility and UI / UX had no pool set, and the Town Hall is skipped. No two buildings on one goal disagree, so no conflict is logged. **Nothing changes in effect:** every building stays in General at the default 1,000,000 tokens/day.

- PR: https://github.com/mitchellgordon95/muster-town/pull/160, merged as **eadf7de**. Redeploy queued, so eadf7de should be live next. I have not checked it live.
- Crop (web mock, 203 px): mf_ef1cqsit5i shows the goal tree Funding block on "Join", with the exploration budget inherited from the root.

## Findings
- **Migration 065** (additive): `goals` gains nullable `poolId` and `explorationTokensPerDay`. Where two buildings on one goal disagree, the first by createdAt wins and the other is logged as a `bank.pool` event (`backfillConflict`). Each goal that receives a value gets a `goal.edited` event so its history shows it. The building columns stay but nothing reads them; the schema comment says so.
- **Resolution:** one helper in core/src/goals.ts, `fundingAt` / `fundingOf`. `Bank.poolOf` uses it, and so do `buildingsIn`, the shares and `/api/finance/pools`; `grantDesk.exploration` uses it too. The Town Hall keeps its special case: no exploration allowance.
- **API:** `PATCH /api/goals/:id` takes `poolId` (admin only) and `explorationTokensPerDay`; the building PATCH no longer takes either. `GET /api/goals` and `/api/goals/:id` return the effective `funding`. `GET /api/bank` adds `pools[].goals` and `buildings[].poolGoalId`. A pool can now be deleted only when no goal names it.
- **Permission change to note:** `explorationTokensPerDay` used to need `building.fund` on a building. On a goal it needs `goals.edit` there plus `building.fund` town-wide or ownership of the goal, so a building's human manager who neither owns the goal nor is an admin can no longer set it.
- **Tests:** new core tests cover the back-fill (including a conflict and the skipped Town Hall), inheritance up the tree, the goal history, and the permissions. I moved the bank, lanes, grants, forks and server REST tests onto goals using two test helpers, `fundBuilding` and `fundGoalOf`. `npm run check --fast` passes (exit 0, 4m39s).
- **Docs updated:** goals.md (an "interim step" note under Finance), bank.md, goal-directed-budgets.md, manual.md, architecture.md, README.md and log.md. I rewrote the topic page "Bank and token accounting" ([dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md)).
- **Not checked yet:** the Funding controls when signed in as admin, and the Bank Pools tab. Both still need a live check on eadf7de with a human session.

## What I need from you
Nothing needed.
