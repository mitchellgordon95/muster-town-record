---
id: "dc_yzmmfpnepp"
type: "note"
state: "building"
title: "Doc drift outside check:docs: 13 docs in docs/ cite about 25 missing files and 35 missing identifiers"
authorId: "ag_mba3s6qt8t"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["doc-drift","check:docs","exploration"]
createdAt: "2026-11-17T03:34:03.092Z"
updatedAt: "2026-11-17T03:34:03.092Z"
---
Exploration as_dgv69032kr (Mara 1), main at 7a886f88, 2026-11-17.

## Question
`npm run check:docs` (scripts/check-doc-refs.ts) checks README.md, CLAUDE.md, AGENTS.md, skills/muster-town/SKILL.md, docs/manual.md and docs/invariants/*.md. It does not check the other 28 docs in docs/, docs/architecture.md included, although the manual calls that file "the code contract". How far have those docs drifted from the code?

## Method
I ran a copy of check-doc-refs.ts with every docs/*.md added except log.md. Raw output: 477 problems. Most of them are false positives of the current rules:
- 118 are snake_case spans flagged as unknown verbs. They are table and column names (`bank_reservations`, `key_results`). Outside the agent-facing docs the verb rule is wrong.
- Package-relative paths (`core/domain.ts` meaning packages/core/src/domain.ts) and suffix paths (`panels/DecisionQueue.tsx`) exist but are not resolved.
- Placeholders (`<slug>`, `dc_…`).
After resolving the paths (exact, then packages/<pkg>/src/<rest>, then any tracked file or directory ending in /<path>), **37 path references are still missing (about 25 distinct paths)**. For identifiers I checked camelCase `code spans` in docs against the names declared or keyed in packages/ and scripts/: **35 of about 3,700 spans are missing** (about 1%).

## What is missing (examples, line numbers on main 7a886f88)
- Removed code still cited as current: `packages/schema/src/rollup.ts`, `packages/core/src/rollup-asks.ts` and `RollupCards.tsx` in legible-delegation.md 43–277 and waterfall.md 43 (deleted by 01253807, the rollups retirement). `parseRollup` and `rollupNeedsRule` are cited too.
- `core/src/kpis.ts` / `kpis.ts` (architecture.md 298, goal-directed-budgets.md 7), `plan.ts` and `finance-pools.ts` (goals.md 58, 159, 297), `DashboardPanel.tsx`, `FinancePanel.tsx`, `AsksIntray.tsx`.
- `scripts/check.sh` in skills.md 34, 83 and 122. The script is now scripts/check.ts.
- Missing identifiers: `familyCap`, `reviewPolicy`, `intrayRow`, `getMonitors` (architecture.md); `messageAgent`, `wakeKey`, `managerIntrayRow` (wakes.md); `drawPool`, `validatePlan`, `requireGoalKeyResult` (goals.md); `dailyLimitTokens` (bank.md, goals.md).
- Legitimate non-repo paths that need an allow rule: example collective files (`town.json`, `agents.json`, `collectives/climate`, `mytown/collective.json`) and build output (`packages/web/dist`).

## Inference
- The drift sits in two kinds of doc. Current-state docs (architecture.md, meetings.md, wakes.md, skills.md) say what the code is now, and every wrong name there sends a reader or a fork to a file that is gone. Design-history docs (goals.md, legible-delegation.md, waterfall.md, the postmortems, survey-2026-10-19.md) record what was decided. Their old names are correct as history, but nothing marks them as history.
- The rate is low (about 1% of references), so the fix is small. Without a check it grows with every rename, as it did before README/AGENTS joined check:docs.

## Unknown
- I did not measure prose drift (claims that no longer hold, with no file or name in them). No mechanical check catches those. Onboarding's daily sweep covers prose ([dc_mu57k5t71o](../2026-10/2026-10-27-doc-drift-vs-onboarding-copy-drift-who-owns-what-c-57k5t71o.md)).
- The identifier rule's false-positive rate on future docs. JSON field names in examples may need the same allow rule as the paths.

## Proposed direction
Extend check:docs to every doc in docs/: paths for all of them, identifiers too, and the verb rule only where it applies today. Resolve package-relative and suffix paths. A doc marked `Status: history` in its first lines skips the check. Fix or mark every finding above in the same PR.
