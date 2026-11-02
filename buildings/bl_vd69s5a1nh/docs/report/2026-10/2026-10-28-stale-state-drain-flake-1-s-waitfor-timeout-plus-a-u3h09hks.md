---
id: "dc_jfu3h09hks"
type: "report"
state: "building"
title: "Stale-state drain flake: 1 s waitFor timeout plus a redeployer-outlives-DB race; 0/50 local repros (dc_cbqaoo4qb9)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_l59kklky3v","dc_cbqaoo4qb9","dc_bp0drrs0ao"],"urls":["https://github.com/mitchellgordon95/muster-town/actions/runs/40454959781"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. Root cause pinned (vi.waitFor 1 s timeout, since widened to 15 s in 07f7957; plus runtime.stop() not waiting for the redeployer's in-flight drain, so cleanup closes the DB under it and the .catch at redeploy.ts:443 rethrows as an unhandled rejection). The fix is step 3 of gr_x5gnnmo7yi, which Mitchell decides in the in-tray; it touches runtime code (Workshop's), so it runs only after funding plus Mitchell's word. Nothing to do until then."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-28T18:04:21.229Z"
sessionId: "se_f9g0jwvwj3"
assignmentId: "as_u9ec6c7okc"
costUsd: 0.9377396
tokens: 46887
turns: 27
createdAt: "2026-10-28T18:03:34.508Z"
updatedAt: "2026-10-28T18:04:21.229Z"
---
## What I did
- Read the failed log of run 40454959781 (commit 8a7a7ca), the drain path in runtime/src/redeploy.ts, `runtime.stop()` and the test cleanup in helpers.ts.
- Ran the test file 50 times: 20 on main, 20 with the old 1 s waits, and 10 with the old waits under CPU load.
- Filed the findings note [dc_cbqaoo4qb9](../../note/2026-10/2026-10-28-stale-state-drain-flake-run-40454959781-reproducti-qaoo4qb9.md). No code changes; my tree is clean. I cut the session short because a redeploy is waiting on it.

## Findings
- **Reproduction: 0 failures in 50 runs.** The test takes about 260 ms idle and 680–800 ms under 2x CPU load. On CI it took 1273 ms. My full-suite runs under heavier load timed out and gave no usable result.
- **The failure itself was a timeout.** It is the facilitation drain test, stale-state.test.ts:117, waiting for `exit(75)`. vi.waitFor's 1 s default ran out before the drain plus the meeting end plus the exit finished. Commit 07f7957 (already on main) raised the waits to 15 s, which hides this but doesn't remove the dependence on wall-clock time.
- **The race behind "database connection is not open" is still on main.** `runtime.stop()` (index.ts:579) does not stop or wait for the redeployer's run that is still in progress. The cleanup then closes the DB while the drain loop keeps polling. The drain throws, the `.catch` at redeploy.ts:443 tries to log the failure to the closed DB and throws again, and the result is an unhandled rejection that vitest blames on the wrong test.
- **Fix (step 3 of the kr_cm5qb2wqh7 proposal), about 20–30k tokens:**
  - add a way to stop the redeployer, and have `runtime.stop()` wait for it;
  - guard the logging call in that `.catch`;
  - add a regression test that stops the runtime mid-drain.

  This is runtime code, so Workshop's OK is needed first.
- No commit of mine is waiting on the redeploy.

## What I need from you
Nothing needed.
