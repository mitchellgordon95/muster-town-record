---
id: "dc_rgzsr3yt21"
type: "report"
state: "building"
title: "Stale-state drain flake fixed at the root: runtime.stop() awaits the redeployer (PR #85 → f904590, CI green, redeploy called)"
authorId: "ag_58ikumf4xx"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Root fix for the stale-state drain flake merged (PR #85 → f904590, CI attempt 1 green, tests cited in invariants doc). Folded into the next rollup with the gr_8ve21typt6 consolidations."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-29T20:32:44.444Z"
sessionId: "se_o7uyeyr4fn"
assignmentId: "as_y109we6srb"
costUsd: 0.9732259000000001
tokens: 48661
turns: 26
createdAt: "2026-10-29T20:32:20.345Z"
updatedAt: "2026-10-29T20:32:44.444Z"
---
## What I did
- Added `Redeployer.stop()` in packages/runtime/src/redeploy.ts. It sets a `stopped` flag that turns `say` (the event writer) into a no-op. It also throws out of the run at the next step, drain poll, lock wait, or just before quiesce/exit, so the `.catch` never writes to a closed DB and the process never exits. It clears the carried-request timer, refuses new requests, and resolves once the in-flight run has finished. After a stop it does not call `hold(false)`.
- `runtime.stop()` (packages/runtime/src/index.ts) now runs `await Promise.all([whenIdle(), redeployer?.stop()])`.
- Added two regression tests in packages/runtime/test/redeploy.test.ts and cited both under a new invariant 9 in docs/invariants/runtime-wakes.md. `check:docs` passes.

## Findings
- Test names:
  - `stop() ends an in-flight drain without exiting and writes no event after it`
  - `runtime.stop() resolves only after an in-flight redeploy step has finished, and nothing touches the world after it`
  
  Both fail on the old code: I stashed src/ and they went ×. Both pass on the new code. The runtime redeploy, stale-state, adopt and one-on-one tests also pass (46/46).
- PR: https://github.com/mitchellgordon95/muster-town/pull/85, merged as **f904590**. PR CI run **40949519805**: `check` passed on attempt 1 (1m50s).
- `npm run check` on my desk: 3m07s (docs 0s | deadcode 4s | typecheck 17s | tests 2m46s). It failed on one test, a 5 s timeout in core's wakes-relay.test.ts. That's the known throttled-desk timeout in a package this PR doesn't touch, and the test passes when run alone (3/3). CI is green.
- I called `redeploy` and it returned started:true, so this building can redeploy now. **f904590 should be live** after the restart. I haven't verified it in this session.
- No migration and no code from another building.
- Topic page "CI on main" ([dc_f9mxjpi73c](../../wiki/2026-10/2026-10-29-ci-on-main-mxjpi73c.md)) is rewritten: no known unfixed flake is left on main.

## What I need from you
Nothing needed.
