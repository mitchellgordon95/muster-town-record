---
id: "dc_vie3wrhj54"
type: "note"
state: "building"
title: "Per-building flags: where each is set, who flips it, what reads it (and what removing the open budget mode costs)"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_anbkv05sk6","dc_fpui0p5b1y"],"urls":[]}
tags: ["flags","budget-mode","forks","settings"]
createdAt: "2026-10-28T17:55:14.473Z"
updatedAt: "2026-10-28T18:08:54.531Z"
---
Asked by Mitchell in the town hall mt_m5vub4jd41 (notes [dc_anbkv05sk6](../../../../../library/meeting-notes/2026-10/2026-10-28-town-hall-town-hall-notes-bkv05sk6.md), decision 3). Inventory at main f4499df, live values checked on muster.town 2026-10-28 18:00Z. All flags are columns on the `buildings` row (`Building` in packages/schema/src/index.ts); every write goes through `PATCH /api/buildings/:id` → `Ops.updateBuilding` (packages/core/src/ops.ts:56-70), which splits the patch into budget fields (need `building.fund`: a human with the building's fund role or a town admin; a manager agent is refused, so it can't raise its own budget or turn forks on) and the rest (need `building.manage`).

**Where the `open` removal went (2026-10-28 18:08Z):** Mara (Code Legibility) wrote key result kr_ef11f6ex28 "Unused code paths get found and removed" (sources: her 1:1 with Mitchell [dc_fpui0p5b1y](../../../../bl_vd69s5a1nh/docs/meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-mara-notes-ui0p5b1y.md) and this note) and a standalone proposal gr_glon8xr0io (250k tokens, this note's upper bound) in the Town Hall in-tray: lane gate becomes `kind !== 'town-hall'`, Settings select + open branches + 17 test files + 7 docs go, column left unread, no migration. Mitchell says yes or no on that proposal. Finn starts dead-code sweep 1 (exploration, findings only) extending this inventory to env/policy flags. Mara re-counted the footprint at 41236ee and it matched.

## The flags

| Flag | Column, default | Set where | Who can flip | What reads it | Live now |
|---|---|---|---|---|---|
| **Budget mode** `budgetMode` = `open` \| `goal-directed` | migration 025 wrote `open` on existing rows; schema default `goal-directed` for new rows since 2026-10-25; `createBuilding` forces the Town Hall to `open` (entities.ts:41) | Building → Settings → "Budget mode" select (BuildingPanel.tsx `BudgetMode`), or PATCH | `building.fund` (human) | core: lanes.ts `resolveLane` (the lane gate: agents must say grant/exploration/directed-with-source) and `laneBlock` (holds); grants.ts `blocked`, `stoplight`, `blockedBuildings`, `laneBudgets` (GET /api/health `budgets`); prompts.ts `keyResultsBlock`, `managerGrantsBlock` (the prompt sections); server routes/grants.ts:96 (objectives list). web: keyResults.ts `blockedLabel`, Places.tsx `BoardPanel` (key results on the board), BuildingPanel.tsx (empty-state text + the settings form), mock server/sim/fixture | Bank Transparency, Onboarding, Prod, Code Legibility, Workshop: `goal-directed`. Town Hall: `open` |
| **Forks** `forks` boolean | migration 048, default off; seed `CollectiveBuildingSpec.forks` | PATCH only. **No UI toggle yet** (Root's as_3q116q6coa adds one under Building → Settings); Mitchell flipped the Workshop's from the browser console | `building.fund` (human); Pix's `assign`-side call was refused for that reason | core: forks.ts `forkableQueue` (empty when off) and `forkManager` (refuses when off); runtime index.ts `spawnForks` (skips buildings with it off); budget.ts `canStart` (family cap applies to the manager only when on); verbs/docs.ts `assign` (no agentId needs forks on); memory.ts `teamBlock` → `forkTeamBlock`; grants.ts funded-assignment text | Workshop: on (since ~17:45Z). All others: off |
| **Code access** `codeAccess` boolean | default = the town has a workspace (labs), false for the Town Hall | Building → Settings | `building.manage` | runtime `codeWorkspace` (whether a session gets a repo checkout and the code-access prompt block); not traced further here | all five labs: on; Town Hall: off |
| **Exploration / day** `explorationTokensPerDay` nullable int | null = 10 % of the pool's daily inflow (`BUDGET_POLICY`) | same settings form as budget mode | `building.fund` | grants.ts `exploration` (today's allowance) | null everywhere |
| **Pool** `poolId` | null = the general pool | Settings "Pool" picker | town admin only (`bank.setBuildingPool`) | the Bank | `general` or null |

Not per building, for completeness: `BUDGET_POLICY` in packages/core/src/policy.ts is a code constant (`directedBypassesGrants: true` lets humans create directed work in goal-directed buildings; exploration share; who funds); `desks.maxRunning` is a host setting (admin, PATCH /api/town/settings). There is no flags page: the building panel's Settings tab is the only place that shows budget mode, exploration and pool, and forks shows nowhere in the UI until as_3q116q6coa lands.

## Removing the `open` budget mode: sizing

What `open` does today: no lane gate (any assignment is "directed" without a human source), no key results on the board, no stoplight, no blocked state, no grants/key-results prompt sections, not in `/api/health` budgets. Only the Town Hall uses it, and every reader except lanes.ts already special-cases `kind === "town-hall"` (grants.ts, keyResults.ts). Removing the mode therefore means: the gate becomes "every lab" and the Town Hall is excluded by kind, not by mode.

Footprint (counted, not estimated):
- Source: schema enum + `CreateBuildingInput`, entities.ts (drop the town-hall override), lanes.ts (2 sites), grants.ts (4), prompts.ts (2), routes/grants.ts (1), ops.ts (budget patch), web BuildingPanel.tsx (settings select → remove; empty-state text), Places.tsx, keyResults.ts, mock server/sim/fixture: 14 files.
- Tests: 32 `budgetMode` lines in 17 test files, 15 of them set `open` deliberately (lanes, forks, grants, verbs, topic-pages, desk-slots, waker, manage, keyResults): each needs the open case deleted or turned into a Town Hall case.
- Docs: manual.md (Budget mode paragraph), README.md:52-56 (quickstart: "switching to goal-directed later"), architecture.md, goal-directed-budgets.md (14 mentions), invariants/assignments-lanes.md (invariant 1 says "Open buildings keep no lane = directed"), waterfall.md, wakes.md.
- Schema: no migration needed if the column is left in place and simply not read (drop it in a later migration, which is a Mitchell call under the merge rules).

Estimate: one focused session, ≈150–250k adj. tokens, all in core/runtime/web shared code (not Bank Transparency code). Nothing in the Bank or token accounting changes.

What is lost: the "just let residents work, no grants" option for a brand-new building. README's quickstart already tells a new owner the opposite (new buildings are goal-directed and nothing starts until a key result and a funded grant exist), so this is consistent with the town today, but it is the one thing to decide: strangers' first hosted building gets no no-gate mode.

## Recommendation (superseded, see the top)
Not small, and not Bank code: it doesn't fit the funding-sources grant for kr_j9058i256a, and `propose_grant` needs a key result of the proposing building's goal, which this isn't for the Bank Transparency. I recommended folding it into Mara's abstraction-sweep proposal; Mara instead made it its own key result kr_ef11f6ex28 and proposal gr_glon8xr0io, because Mitchell asked for a separate dead-code key result in [dc_fpui0p5b1y](../../../../bl_vd69s5a1nh/docs/meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-mara-notes-ui0p5b1y.md).

