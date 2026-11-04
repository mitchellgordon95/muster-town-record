---
id: "dc_9quo2utt6x"
type: "report"
state: "building"
title: "gr_7op2v8fjcl red-main edge cases: a failed deploy job or a cancelled run read red; fixed in PR #343, parked on CI"
authorId: "ag_5e9sxuqf44"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #343 (mainStateOf: red only on a failed code check; cancelled check = pending; promote/image ignored) is the right reading for a fixer that can only fix code. The merge is already queued as as_neh2zj9olz waiting on {pr: 343}; nothing more to assign. Behaviour change (a failed deploy no longer shows in `main`, only as /api/health commit lag) goes in the next rollup's item for gr_7op2v8fjcl."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-04T19:27:52.919Z"
sessionId: "se_eqsjd2vy7z"
assignmentId: "as_dh0rv1hv0f"
costUsd: 1.0239839000000002
tokens: 51199
turns: 22
createdAt: "2026-11-04T19:27:43.461Z"
updatedAt: "2026-11-04T19:27:52.919Z"
---
## What I did
I read the merged step-2 code on origin/main (ed953de is in it): `packages/runtime/src/pr-checks.ts` `readMain`, and `packages/core/src/main-fix.ts` `queueMainFix` and `mainRedLine`. I wrote one test per edge case. Both tests fail on main as it is. I fixed the code in one small PR: https://github.com/mitchellgordon95/muster-town/pull/343 (draft). `npm run check` passes on my desk (335 tests in the last package; total 6m31s). I rewrote the topic page "CI on main" ([dc_f9mxjpi73c](../../wiki/2026-10/2026-10-29-ci-on-main-mxjpi73c.md)). The work is parked on PR #343's CI.

## Findings
- **Case 1 was wrong.** If `check` passed but `promote` or `image` then failed or was cancelled, main read **red** with failedStep "promote" and queued a fix assignment. Nothing in the code was broken. Cause: `readMain` counted any run outside success/neutral/skipped, plus the suite conclusion, as bad.
- **Case 2 was half right.**
  - A running main stays pending and is safe: `queueMainFix` returns unless state is red (main-fix.ts:59), and `mainRedLine` is null unless state is red (main-fix.ts:107).
  - A `check` run cancelled by the next push read **red** if the poll saw the cancelled run before the new head. The fixer would then be queued for a run that was only superseded.
  - On a busy main this can happen. As of origin/main 2efd241, ci.yml still has `cancel-in-progress: true`.
- **Fix (PR #343):** a new function `mainStateOf` in pr-checks.ts:
  - main is red only when a code check failed;
  - a cancelled code check reads pending;
  - `promote` and `image` results are ignored, so the head reads green once `check` passed.
- **Tests added** in `packages/runtime/test/pr-checks.test.ts`, both named in invariant 10 (docs/invariants/runtime-wakes.md):
  - "a failed or cancelled deploy job (promote, image) after a passed check is not red…": also checks that a failed check next to a failed deploy job is red and names only "check";
  - "a busy main stays pending…": five merges, each read while running and again after being cancelled. The result is one pending stretch, no fix assignment, and no author read.
- **What changes for the live town:** a failed deploy is no longer reported in `main`; it shows only as /api/health `commit` lagging.

## What I need from you
Nothing needed.
