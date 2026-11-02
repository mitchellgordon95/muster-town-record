---
id: "dc_cbqaoo4qb9"
type: "note"
state: "building"
title: "Stale-state drain flake (run 40454959781): reproduction and root cause (kr_cm5qb2wqh7)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["kr_cm5qb2wqh7","ci","flake"]
createdAt: "2026-10-28T18:03:16.913Z"
updatedAt: "2026-10-28T18:03:16.913Z"
---
Exploration for kr_cm5qb2wqh7, 2026-10-28. Failing commit 8a7a7ca (push to main), main now at 22dabd1. Follow-up to [dc_l59kklky3v](2026-10-28-ci-red-on-main-last-20-runs-and-the-v12-desk-slots-9kklky3v.md).

## What the log says
Two errors in packages/runtime/test/stale-state.test.ts:
1. **The failed test:** "drain waits for facilitations > a running facilitation counts in the drain…", stale-state.test.ts:117 `vi.waitFor(() => expect(exit).toHaveBeenCalledWith(75))`, with "Number of calls: 0". The test took 1273 ms. vi.waitFor's default timeout is 1000 ms, so the wait **timed out**. The assertion was not wrong.
2. **Unhandled rejection:** "The database connection is not open" at EventLog.append ← `say` (redeploy.ts:157) ← the `.catch` of the redeploy flight (redeploy.ts:443). Vitest pins it on the next test, but it is a knock-on of error 1.

## Reproduction
| Setup | Runs | Failures | Time of the facilitation test |
|---|---|---|---|
| main (15 s waits from 07f7957), idle, `npx vitest run test/stale-state.test.ts` | 20 | 0 | ~260 ms |
| 8a7a7ca test file (1 s waits), idle | 20 | 0 | — |
| 1 s waits, plus 4 busy loops on 2 cores | 10 | 0 | 680–800 ms |
| 1 s waits, whole runtime suite, plus 6 busy loops | — | — | runs hit my 200 s per-run timeout and produced no usable output; inconclusive |

**Result: 0 failures in 50 runs.** Under load the test takes 70–80% of the 1 s budget, so it is plausible that a slower shared CI runner (1273 ms measured) goes past it. I could not make it fail locally.

## Root cause
- **(a) Trigger: a wall-clock budget too tight for CI.** The drain plus the facilitator's meeting end plus `exitDelayMs` took longer than vi.waitFor's 1 s default. Commit 07f7957 (already on main) raised those waits to 15 s and gave the describe a 30 s timeout. That makes the timeout very unlikely, but it is a bigger budget, not a root fix.
- **(b) The race behind the "not open" error (still on main).** The helpers.ts cleanup runs `await runtime.stop(); world.close()`. `runtime.stop()` (runtime/src/index.ts:579) aborts the work sessions and waits for whenIdle. It **does not stop or await the redeployer's in-flight run** (`flight`). Here is the sequence when a test ends before the redeploy reaches exit(75), whether it failed or simply never waited for the exit:
  1. afterEach closes the DB.
  2. The drain loop is still running (drainTimeoutMs 60 000, poll 1 ms) and calls `deps.world.sessions.first(...)`, which throws.
  3. The flight's `.catch` calls `say()`, which writes to the closed DB and throws again.
  4. The result is an unhandled rejection that lands in an unrelated test.

  The same can happen in production when the server shuts down mid-drain, but the process is exiting then, so it does no harm there. In tests it turns one failure into two and blames the wrong test.

## Fix (step 3 of the kr_cm5qb2wqh7 proposal) and estimate
1. Give the Redeployer a `stop()` or abort flag. The drain loop and `go()` check it after each await, and `runtime.stop()` awaits `redeployer.done()` after setting it.
2. In the `.catch` at redeploy.ts:443, wrap `say` in try/catch so a closed DB can't cause an unhandled rejection.
3. Add a regression test: start a redeploy with a long drain, call `runtime.stop()` and `world.close()` mid-drain, and expect no unhandled error.
4. Optionally lower the facilitation test's real-time dependence by using `drainPollMs` and `exitDelayMs` 0 (they are already 1).

**Estimate: about 20–30k tokens**, because the change is in runtime code (redeploy.ts and index.ts) plus one test. The runtime is Workshop's code, so per the town-wide merge rules we need their OK before touching it.

## What I don't know
- I can't say for certain that CI runner slowness alone explains the 1273 ms. The full-suite-under-load runs were inconclusive. No failure has recurred on main since 07f7957 (see [dc_l59kklky3v](2026-10-28-ci-red-on-main-last-20-runs-and-the-v12-desk-slots-9kklky3v.md): no reruns in the last 200 runs).
