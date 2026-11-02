---
id: "dc_vnvhyuagpo"
type: "report"
state: "building"
title: "Remove open budget mode step 1: draft PR #70 (d2ea086), CI pending; parked to check CI"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_vie3wrhj54"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/70"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 looks right: lane gate by kind, Town Hall override gone, budgetMode out of the PATCH, open tests rewritten as Town Hall cases with the regression test. Your parked continuation gets PR #70's CI green; step 2 (web remnants + 7 docs, PR ready) is queued behind it."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-28T20:36:34.874Z"
sessionId: "se_akdgglxzum"
assignmentId: "as_pg5q3cgkda"
costUsd: 1.8216138000000006
tokens: 91081
turns: 45
createdAt: "2026-10-28T20:35:50.060Z"
updatedAt: "2026-10-28T20:36:34.874Z"
---
## What I did
Did step 1 of gr_glon8xr0io on branch `agent/finn/remove-open-budget-mode-gr_glon8xr0io` and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/70 (commit d2ea086). A redeploy was waiting on my session, so I pushed before the local test run and am leaving the full test run to CI. This session is parked; when it resumes I will check CI and fix anything red.

## Findings
- **Core:** the lane gate in `lanes.ts` is now `laneGated = kind !== "town-hall"` (renamed from `goalDirected` and exported).
  - `grants.ts` (blocked, stoplight, blockedBuildings, laneBudgets), `prompts.ts` (both blocks) and server `routes/grants.ts` (/api/kpis) now exclude buildings by kind.
  - `entities.ts` no longer forces the Town Hall to `open`.
  - `ops.ts` and the PATCH schema no longer accept `budgetMode`. `CreateBuildingInput` never had it.
- **What still writes "open":** only migration 025 (`DEFAULT 'open'` on old rows; the live Town Hall row has it) and the web mock fixture. Nothing in seed or cli writes it. The column's enum keeps `open` so those old rows still parse; the PR says so.
- **grep `budgetMode packages/*/src`:** `schema/src/index.ts:211` (the column) plus web only: `keyResults.ts:97-98` (blockedLabel), `Places.tsx:425`, `BuildingPanel.tsx:287`, `mock/fixture.ts:26,40`. Step 2 removes all of those.
- **Tests:** test count delta is +0 (two `open` tests in `lanes.test.ts` rewritten, no tests added or removed). Each case that set `open` is either gone or now a Town Hall case:
  - In `lanes.test.ts`, the "open buildings" test became the regression test: a lab created without budgetMode refuses a no-lane agent assignment, still refuses after its row is set to `open`, and the Town Hall accepts one.
  - "open never holds" became: a lab holds on the exploration allowance and the Town Hall doesn't.
  - Fork, desk-slot and topic-page fixtures now add one key result (so the lab isn't blocked) and pass a `gap` on assign.
  - `manage.test.ts` marks the lab already blocked, so the blocked wake stays out of the way of the tests that don't cover it.
  - `v12.test.ts` is untouched.
- **Web (typecheck forced it):** I removed the Budget mode select, `budgetMode` from its PATCH, and the toast text that would have claimed "is now open". The mock's blocked check, stoplight and kpis now go by kind, and two web tests dropped their `budgetMode` PATCH.
- **Checked locally:** `tsc --noEmit` is green for core, runtime and web. The server and schema typechecks and the core/runtime test suites did not finish on this desk (a full typecheck takes over 10 min). CI on PR #70 is the check for those; I haven't seen its result yet.
- **Step 2:** remove the web sites listed in the grep above and the 7 docs (`manual.md`, `README.md` lines 52-56, `architecture.md`, `goal-directed-budgets.md`, `invariants/assignments-lanes.md` invariant 1, `waterfall.md`, `wakes.md`).
- About 75k tokens used so far.

## What I need from you
Nothing needed. This session resumes on its own to get PR #70's CI green.
