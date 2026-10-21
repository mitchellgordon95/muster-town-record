---
id: "dc_u2gknsn3my"
type: "report"
state: "building"
title: "Budgets step 1a pushed (7bef911): grant/KR schema + tables, building.fund guard; grant CRUD/decide next"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T03:10:20.923Z"
sessionId: "se_5nqmw3lqnt"
assignmentId: "as_dere9buanq"
costUsd: 1.5542471000000002
tokens: 3113101
turns: 38
createdAt: "2026-10-21T02:12:34.342Z"
updatedAt: "2026-10-21T03:10:20.923Z"
---
## What I did
I started rollout step 1 of the goal-directed budgets design ([dc_k955hun6c4](../../article/2026-10/2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md)). A redeploy was waiting for my session to end, so I stopped after the foundation. That part is committed and pushed to main as **7bef911**, and I requested a redeploy. **7bef911 should be live after the restart.** I'll check that next session.

## Findings
- **Schema** (`packages/schema`): new `SpendLane`, `Grant` (with its negotiation history), `KeyResult` and `GrantView` (a grant with its key results and spend). Also the inputs for creating, editing, deciding and closing grants and for updating key results, and new `grant.*` and `kr.updated` events.
- **Migration 025**: new tables `grants` and `key_results`. Sessions get `lane` and `grantId`, so a grant's spend can be computed as the sum of its sessions' tokens instead of kept in a second counter. Buildings get `explorationTokensPerDay` (null means 10% of the pool's daily inflow) and `budgetMode` (default `open`, so no building changes yet).
- **`building.fund` permission**: admins have it, and so do built-in building managers (`migrateRoles` adds it to existing manager roles on the next start). It never applies to agents, except a human's own avatar acting for that human. So an agent manager whose owner is an admin still can't fund its own proposal.
- **One change from the design**: setting `explorationTokensPerDay` or `budgetMode` on PATCH building needs `building.fund`, not `building.manage`. Otherwise a manager agent could raise its own exploration allowance.
- **New Bank helpers**: `Bank.dailyInflow()` and `poolDailyInflow(poolId)` give the inflow the 10% default is based on. Today that's 20,000,000 tokens/day for General, so 2,000,000 per building.
- **Verified**: typecheck is clean, and all tests pass (core 207, including the new `grants-schema.test.ts`; server 59; runtime 74).
- **Not built yet (rest of step 1)**: the grant service (create a draft with 2–3 key results, edit, propose with one open proposal per building, decide fund/counter/reject and continue/adjust/cut, close, key-result status rules, today's exploration allowance and spend), its REST routes, and tests.

## What I need from you
Nothing needed. Next session I'll check that 7bef911 is live, then build the grant service and its routes to finish step 1.
