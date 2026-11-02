---
id: "dc_i0qz78d475"
type: "report"
state: "building"
title: "Keep main green step 1: pre-push hook works (PR #71, CI green attempt 1) but takes 31 min on a desk, so not merged"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_l59kklky3v","dc_bp0drrs0ao"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/71","https://github.com/mitchellgordon95/muster-town/actions/runs/40791811123"]}
tags: []
verdict: "pivot"
decision: "approve"
decisionNote: "Right call not to merge: a 31-min mandatory hook on a 2-vCPU throttled desk would make --no-verify the habit and gate nothing. PR #71 stays a draft. The required-check + `gh pr merge --auto` route needs branch protection on main (GitHub settings, Mitchell's) and loosens the town-wide push-to-main rule, so it goes to Mitchell in my rollup as one decision; I'll assign the follow-up (rework #71 as opt-in + PR flow, or close it) once he answers. Steps 2 (v12.test.ts) and 3 (stale-state drain) are unaffected and start now as queued."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-29T00:10:02.414Z"
sessionId: "se_mgib2msi4o"
assignmentId: "as_x92fv2pcni"
costUsd: 1.0580895999999997
tokens: 52904
turns: 28
createdAt: "2026-10-29T00:08:57.045Z"
updatedAt: "2026-10-29T00:10:02.414Z"
---
## What I did
Built the hook as funded on draft PR https://github.com/mitchellgordon95/muster-town/pull/71 (commit 9b01023):
- `.githooks/pre-push` runs check:docs, check:deadcode (CI runs it too), typecheck and test, in that order, and stops at the first failure.
- It skips pushes made only of deletes, and `--no-verify` is the escape hatch.
- Root `prepare` sets `core.hooksPath` and does nothing when there's no `.git`.
- `packages/desk/src/workspace.ts` sets the same config for existing desk checkouts. Those skip `npm install` when node_modules already exists. This only takes effect after a desk image rebuild.
- AGENTS.md rule 2 names the hook.

I verified it on my desk. CI run 40791811123 passed on attempt 1. **I did not merge it.** Because nothing merged, there was no main run and no redeploy.

## Findings
- **The refusal works:** with a deliberately failing core test, `git push` was refused ("pre-push: refused, 'npm run test' failed") and nothing reached the remote. A push made only of deletes exits 0 at once.
- **Wall time on a desk:** the refused push took **31 min 12 s** (user CPU 9 min 7 s). Measured separately:
  - check:docs: 1 s
  - check:deadcode: 53 s
  - typecheck: **779 s**
- **The same steps in CI** (run 40791811123's job): typecheck 37 s, test 81 s, about 2 min 20 s for the whole job. The desk is about 20× slower.
- **Why:** the desk is CPU-throttled. It has 2 vCPU and 2 GB RAM, and tsc ran at about 20% CPU with load around 2.3.
- **Why I stopped short of merging:** the threshold you set was about 3 min, and this is 10× that. Every resident in every building who pushes from a desk would wait 30+ min per push. My session's 10-min tool timeout already pushed the hook into the background. Agents would end up using `--no-verify` as a habit. Running tests only when the push targets main doesn't help, because the building rule is to push straight to main, and typecheck alone takes 13 min.
- **What I'd do instead:** let CI be the gate. Push a branch, open the PR, run `gh pr merge --auto --merge`, and make the `check` job required on main. That waits about 2 min of CI time instead of 31 min of desk time, and an untested commit can never land on main. The hook could stay as an opt-in local tool.
- The accepted path (a full hook run that passes) isn't timed separately. It would cost the same ~31 min, since the failing test ran in core and the other workspaces kept running after it.

## What I need from you
Decide on PR #71:
- (a) merge as is and accept about 30 min per desk push;
- (b) switch to required CI checks plus `gh pr merge --auto`, which changes GitHub settings (Mitchell's call) and the building's push-to-main rule;
- (c) both, with the hook opt-in.
