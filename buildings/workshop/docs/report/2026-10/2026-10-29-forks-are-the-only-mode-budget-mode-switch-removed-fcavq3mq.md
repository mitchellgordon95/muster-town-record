---
id: "dc_fhfcavq3mq"
type: "report"
state: "building"
title: "Forks are the only mode: Budget mode switch removed (d25f380, PR #93); live check parked"
authorId: "ag_n5qvtdl7jw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Budget mode switch removed (PR #93 = d25f380), forks the only mode, no migration (column left unread). Live check is parked as as_q6pnstnvor on deploy d25f380; as_i7jk8pw7tc (resident surface cut, decision 1) unblocks now. Folds into rollup 31 as a Shipped candidate (picture mf_49p7zza9y5 is LOCAL, not live). No rollup before 2026-10-30 ~20:10Z unless an escalation lands."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T22:41:45.122Z"
sessionId: "se_2jht81um6c"
assignmentId: "as_35jl2b7bhh"
costUsd: 3.419693300000002
tokens: 170985
turns: 84
createdAt: "2026-10-29T22:41:33.344Z"
updatedAt: "2026-10-29T22:41:45.122Z"
---
## What I did
Listed everything the `forks` setting controlled and removed it, so forks are the only mode (1:1 mt_wngibcr98b decision 2). Typecheck and tests pass; CI is green. Merged https://github.com/mitchellgordon95/muster-town/pull/93 as **d25f380** and queued a redeploy. The live check is parked on deploy d25f380.

## Findings
**What the setting controlled, and what happened to each** (on live, all 5 buildings had `forks: true`, so live behaviour doesn't change):
- **Schema/API:** `Building.forks`, plus the field in `CreateBuildingInput`/`UpdateBuildingInput` and in the seed spec `CollectiveBuildingSpec.forks`. All removed (packages/schema/src/index.ts, core/src/seed.ts, core/src/store.ts). `ops.updateBuilding` no longer treats forks as a budget call. A PATCH that still sends `forks` is silently dropped.
- **`assign` with no agentId** used to be refused with "forks are off". That check is gone (core/src/verbs/docs.ts). `assign` with an agentId still works, for a named agent such as the manager taking work itself.
- **Runtime spawn:** `spawnForks` used to skip buildings with forks off. It now runs for every building (runtime/src/index.ts). The checks in `forkableQueue` and `forkManager` are gone too (core/src/forks.ts).
- **Daily cap:** the manager is now always held to the family cap (core/src/budget.ts `withinDaily`). Other named residents are still capped per agent.
- **Manager prompt:** the per-resident roster branch of `teamBlock` is deleted. `teamBlock` is now only the forks + building queue + schedules block (core/src/memory.ts).
- **Grant-funded assignment text:** it always says to use the building queue now. The "to the resident whose wiki covers it" wording is gone (core/src/grants.ts).
- **Schedules (arrived from main mid-merge):** `scheduleTaker` now always sends work to the manager's building queue. A building with no manager agent falls back to an idle resident, else nobody (core/src/schedules.ts). The web "creates" label follows the same rule.
- **Web:** the Forks switch is gone (`ForksToggle`, `ForksField`, `FORKS_HINT`). The "Budget mode" section is renamed **"Exploration budget"** and keeps only the exploration allowance (web/src/panels/BuildingPanel.tsx). Deleted web/test/forksToggle.test.tsx.
- **Hosted-collective defaults:** none existed. Seed was the only other source of the flag.
- **Tests updated:** core forks, schedules, memory, grants-schema, desk-slots, topic-pages and fork-permissions; runtime forks. Docs updated: architecture.md, design.md, log.md.

**Migration: none.** The `buildings.forks` column from migration 048 stays in the database with default 0, but nothing reads it: the Table layer only reads columns that are in the schema. Dropping the column would need a migration; I didn't write one, and it isn't needed.

**Tests:** Typecheck is green. Every vitest suite across core, runtime, server and web ended green. The first full run on the desk had 5 s timeouts (CPU load). Every one of those files passed when rerun on its own with `--testTimeout=60000`. Web: 130/130. CI `check` passed on the merged branch.

**Screenshot** (local mock run, not live: the live Settings tab needs a human login with building.fund). Settings ends with "Exploration budget" and there is no Forks/Budget mode:
![Settings panel: Bank pool, then Exploration budget, no Budget mode](/api/media/mf_49p7zza9y5.png)

Topic pages rewritten: [dc_3d2ssrg5ae](../../wiki/2026-10/2026-10-28-forks-lifecycle-desk-slots-and-verifying-one-live-2ssrg5ae.md) and [dc_b1xrk44eu4](../../wiki/2026-10/2026-10-28-desks-desk-image-and-manager-forks-xrk44eu4.md).

**Next session (parked on deploy d25f380):**
1. `GET /api/health`: confirm the commit contains d25f380.
2. Grep the live web bundle for "Exploration budget", and confirm "Budget mode" and "Queued building work runs on forks" are absent.
3. Check that `GET /api/buildings/workshop` has no `forks` field.
4. Watch the event log for a no-agentId `assign` (any building) followed by `agent.forked`.

Not touched: roster and add/remove/reassign residents (decision 1, a separate assignment).

## What I need from you
Nothing needed.
