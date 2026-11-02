---
id: "dc_wh71cali3c"
type: "report"
state: "building"
title: "Fast check step 1: the 31 min was 89% hypervisor steal; unthrottled desk does the check in 4.5 min, ~3 min with two changes (dc_adxve66v1t)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_adxve66v1t","dc_i0qz78d475","dc_grvhp5dl9l"],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Step 2 (as_fvw2luhkpj, already queued) should build on the two measured levers: typecheck the 6 node packages as one tsc program (15.5 s vs 47 s) and vitest --maxWorkers=2 (139 s vs 199 s), plus incremental tsc and the per-step timing line; projection 177 s cold. Record steal (/proc/stat) alongside each timing in the step 2 report so a throttled run is recognisable. The desk-size call goes to Mitchell in the step 4 close rollup."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-29T04:06:07.251Z"
sessionId: "se_axd93o3du2"
assignmentId: "as_17sydmd1cl"
costUsd: 0.9451781000000001
tokens: 47259
turns: 24
createdAt: "2026-10-29T04:05:29.036Z"
updatedAt: "2026-10-29T04:06:07.251Z"
---
## What I did
On main 2d8694d I timed every CI `check` step on my desk, cold. I also timed each workspace on its own, the warm and repeat runs (incremental tsc, `vitest --changed`, vitest worker count) and a probe that typechecks the six node packages as one tsc program. I compared all of it with the last 5 CI runs on main. `/usr/bin/time` isn't installed on desks, so the timings come from a wrapper that reads rusage, /proc/stat steal and PSI for each command. The full tables are in [dc_adxve66v1t](../../note/2026-10/2026-10-29-fast-check-step-1-desk-timings-cold-vs-warm-and-th-xve66v1t.md). Nothing was merged and the branch has no changes.

## Findings
- **Cold run, unthrottled desk (2 vCPU EPYC, 2 GB):** 269 s (4 min 29 s) in total, summed per step, all tests passing. Typecheck took 59.3 s across 7 workspaces, tests 199.4 s (core alone 87.3 s), knip 6.0 s, check:docs 0.6 s, the web build 4.0 s.
- **Where the 31 min went:** it was CPU time withheld by the host (steal), not slow code. From boot to the start of this session the desk logged 779 s of CPU work and 6,069 s of steal: 89% of the time it was busy, so it delivered about 11% of the CPU the work asked for. During this session steal was 2% (20 s against 1,030 s of work).
  - Memory is ruled out: memory pressure has been zero since boot.
  - tsc used about 1.55 cores, not the 0.5-core ceiling we assumed.
  - My guess, not verified: Fly's shared vCPUs run out of burst allowance under sustained load and get capped.
- **CI `check` job:** about 2 min 20 s (typecheck 24–36 s, tests 58–83 s). That is already under the 3-minute CI target.
- **Levers I measured:**
  1. **Typecheck the 6 node packages as one tsc program:** 15.5 s instead of 47.0 s. Today core is re-checked inside runtime, server and cli.
  2. **Run vitest with 2 workers:** vitest defaults to 1 worker on a 2-vCPU desk, so test files run one at a time. With `--maxWorkers=2` the test suites take 139 s instead of 199 s.
  3. **Incremental tsc:** a repeat run with no change takes 20.9 s (summed over workspaces) instead of 59.9 s. After a one-file change in core it takes 42 s, because the dependent packages are re-checked fully.
  4. **`vitest --changed`:** 5.8 s after a test-file edit, but no saving after a core source edit (69 of 73 files still run).
- **Projection with levers 1 and 2:** about 177 s cold. That meets the 3-minute target, with no margin. After a one-file change: about 4–14 s of typecheck plus about 6 s of tests for a test-file edit, so under 1 minute. A core source edit still re-runs about 59 s of tests, right on the 1-minute line.
- **The desk-size call:** on an unthrottled 2-vCPU desk the code changes reach the target. On a throttled desk nothing in the code can: the same ~4 min of CPU becomes ~30 min. So the question for Mitchell is dedicated vCPU or not; more cores won't fix this.
- **Proposed step 2:** a root `npm run check` that runs tsc once (with incremental), runs vitest with 2 workers, and prints a timing line per step. Worth about 92 s cold, measured. The timing lines also count toward kr_8wilbokqcn.

## What I need from you
Nothing needed. Mitchell's desk-size call (dedicated vCPU vs shared) can be made from the steal numbers above.
