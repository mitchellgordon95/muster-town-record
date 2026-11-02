---
id: "dc_tt1fskf9mq"
type: "report"
state: "building"
title: "Fast check step 2: npm run check with per-step timings is on main (PR #74, 2d4a490, live); CI full check 1m12s; desk runs throttled, so desk targets unproven"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Step 2 done and visible: `npm run check` with the per-step timing line is on main (PR #74, 2d4a490, live), CI check job 1m12s on run 40819679824, broken-test proof in run 40818523011. The desk targets are blocked by hypervisor steal (89–92%), not code; the dedicated-vCPU call goes to Mitchell in the checkpoint rollup (gr_75eq6h3ltp is at 155,390 / 120,000, so step 3 as_jf7kxyetsb is held until he continues or cuts). No re-timing until he answers."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-29T04:56:59.278Z"
sessionId: "se_x2aqir7aoq"
assignmentId: "as_fvw2luhkpj"
costUsd: 1.2283563000000002
tokens: 61418
turns: 34
createdAt: "2026-10-29T04:56:04.167Z"
updatedAt: "2026-10-29T04:56:59.278Z"
---
## What I did
- Built step 1's recommendations ([dc_adxve66v1t](../../note/2026-10/2026-10-29-fast-check-step-1-desk-timings-cold-vs-warm-and-th-xve66v1t.md)): https://github.com/mitchellgordon95/muster-town/pull/74. I merged it as 2d4a490, and `/api/health` shows that commit live.
- `redeploy` was refused (I don't have `town.redeploy`). CI's promote job redeployed instead.
- **`scripts/check.ts` behind `npm run check`.** It runs check:docs, check:deadcode, typecheck and tests in that order and stops at the first failure. It ends with one timing line, e.g. `check: docs 1s | deadcode 3s | typecheck 11s | tests 58s | total 1m12s`. A failed run ends that line with `| FAILED at <step>`.
- **`npm run check --fast`** (or `CHECK_FAST=1`) skips knip and runs `vitest --changed <merge-base with origin/main>`.
- **One tsc program.** A root `tsconfig.json` checks the six node packages as one program, and web is a second program. Root `npm run typecheck` now calls this too.
- **Incremental tsc** in every tsconfig. The cache goes to `node_modules/.cache/tsc` and is not committed.
- **vitest workers:** `--maxWorkers max(2, cpus−1)`, because the default gives a 2-vCPU desk only 1 worker.
- **CI:** the `check` job runs `npm run check`, then the web build. AGENTS.md and README now name `npm run check`. check:docs and knip are green.

## Findings
- **CI, full set.** The PR's first run was green on attempt 1 (40818258304, total 1m52s). Main run 40819679824 on 2d4a490 was green on attempt 1: `docs 1s | deadcode 3s | typecheck 11s | tests 58s | total 1m12s`. The job took 1m27s, against about 2m20s before. Typecheck in CI dropped from 24–36 s to 11–18 s.
- **A broken test turns CI red.** Commit 89817ee added a failing test, and run 40818523011 failed: `check: docs 0s | deadcode 3s | typecheck 12s | tests 1m02s | total 1m18s | FAILED at tests`. Revert e4f089a was green again (2m02s).
- **Desk, cold: 21m39s, but throttled.**
  - Timing line: `check: docs 3s | deadcode 58s | typecheck 6m23s | tests 14m15s | total 21m39s | FAILED at tests`.
  - Hypervisor steal during the run was 2,279 s.
  - The failures were 19 tests hitting the 5 s timeout, all from the throttling. The same tests pass in CI.
  - Typecheck on its own, measured earlier this session at 2% steal, took 28 s cold (it was 59 s).
- **Desk, `--fast` after touching one core test file, on main: 8m09s, also throttled.**
  - Timing line: `check --fast: docs 3s | typecheck 5m49s | tests 2m16s | total 8m09s`.
  - The desk got 73 s of CPU work against 801 s of steal (92%).
  - The mode itself behaved correctly: 1 test file ran, the other 5 workspaces found nothing to run, and knip was skipped.
- **Targets on a desk (3 min cold, 1 min repeat): not shown this session.**
  - The gap is desk CPU, not code. The desk spent 89–92% of its time in steal.
  - From the measured parts (unthrottled typecheck 28 s, step 1's tests with 2 workers ~139 s), I project ~2m55s cold. That is an estimate, not a measurement.
  - The repeat run's CPU work was ~73 s, spread over 2 cores. That points to under 1 min unthrottled, but I haven't timed it.
- **Gotcha:** `--fast` reruns every test when the branch changes any `package.json` or vite config. That's vitest's force-rerun triggers, so PR #74's own branch couldn't use it for the measurement.

## What I need from you
Decide whether desks get dedicated (unthrottled) vCPUs. Without that, a desk timing can't show the 3-min / 1-min targets. With it, I'd re-time both runs in one short session.
