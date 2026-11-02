---
id: "dc_xg2fjhd1gd"
type: "report"
state: "building"
title: "Assignment waits now hold through the awaited work's park chain (PR #170 = 3542270 merged, redeploy queued)"
authorId: "ag_y14492ib3q"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. 3542270 is live inside 8d18dbc (health 19:02Z). Decided line for rollup 35."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T19:20:25.460Z"
sessionId: "se_4yai5zmwp8"
assignmentId: "as_ddi1stjc9q"
costUsd: 1.1283249
tokens: 56416
turns: 27
createdAt: "2026-10-31T18:54:46.517Z"
updatedAt: "2026-10-31T19:20:25.460Z"
---
## What I did
- Changed `waitMet` in core `waits.ts` so a `{assignment}` wait reads the last assignment of the awaited work's park chain, via the new `chainTip`. `blockedBy` now names that continuation.
- Added a test. Updated docs/architecture.md, docs/wakes.md, docs/log.md and the topic page [dc_mhz91klzjk](../../wiki/2026-10/2026-10-28-wakes-and-blocked-assignment-reasons-z91klzjk.md).
- PR https://github.com/mitchellgordon95/muster-town/pull/170: CI green, merged as **3542270**. I queued a redeploy, so **3542270** should be live; I have not checked the health commit yet.

## Findings
- **The rule as coded:** `waitFor` / `resumeWhen {assignment: X}` holds while `chainTip(X)` is pending or active. `chainTip` starts at X and keeps moving to the newest assignment with `fromAssignmentId = current AND parked IS NOT NULL`, which is the park continuation.
  - The wait releases when the chain's last assignment is done without a continuation, or cancelled. A cancel comes from Stop or Redirect on the parked report, or from a wait that expired.
  - A missing X also releases, as before.
- Review follow-ups (Continue or Redirect on a report that did not park) are not followed. Work that ends done with verdict continue still releases the wait, as before.
- There is no schema change: `parked` and `fromAssignmentId` were already stored.
- **Test** (core/test/waits.test.ts, "holds through its parked chain"):
  - Work parks: the wait holds, and the blocker points at the continuation.
  - The continuation runs and parks again: the wait still holds.
  - The last continuation ends with verdict stop: the wait releases.
  - A separate run where Stop on the parked report cancels the continuation: the wait releases.
- Core tests pass (87 files, 534 tests), as do runtime work.test.ts and the typecheck.
- Effect: chained build steps (like steps 3 and 9, [dc_p40y8346at](2026-10-31-step-3-declarative-exploration-parked-step-2-as-1s-0y8346at.md) and [dc_pthfpoe3hm](2026-10-31-step-9-docs-sweep-parked-steps-1-3-not-on-main-yet-hfpoe3hm.md), about 15k tokens each) no longer start once per park. One known limit: if two chains each wait on the other they deadlock, and the 24 h wait expiry cancels them as before.

## What I need from you
Nothing needed.
