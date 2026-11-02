---
id: "dc_pzjxniaq7s"
type: "report"
state: "building"
title: "Cleo stuck \"walking\": a restart dropped his walk home; fixed in PR #120 (8ffc906), redeploy via CI"
authorId: "ag_6y6t73tfcz"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved 2026-10-30 ~19:30Z. Cause (restart mid-walk, walk kept only in memory, \"walking\" status persisted, stayReason keeps him put) and fix (reconcile resets stale \"walking\"; Movement.go no longer restores it) both read right; CI promote handles the redeploy. Your parked continuation as_pzrg63mupx (waitFor deploy 8ffc906) does the live check: confirm Cleo idle at (38,50) and take one cropped picture for rollup 32."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T19:23:00.480Z"
sessionId: "se_vl0rb96s3m"
assignmentId: "as_07k43unbf6"
costUsd: 0.9388691999999998
tokens: 46943
turns: 28
createdAt: "2026-10-30T19:22:41.937Z"
updatedAt: "2026-10-30T19:23:00.480Z"
---
## What I did
Read Cleo's record from GET /api/town and his events from GET /api/events, then found the cause in core/world/movement.ts and core/home.ts. I fixed it with two tests (both fail without the fix and pass with it), opened PR #120 (https://github.com/mitchellgordon95/muster-town/pull/120), waited for CI to pass and merged it as **8ffc906**. CI's promote job pushes it to prod and redeploys, so I did not call redeploy. Topic page: [dc_xc22yokhgh](../../wiki/2026-10/2026-10-30-bodies-stuck-walking-after-a-restart-22yokhgh.md).

## Findings
- **What the live town showed (19:14Z, live f402bcf):** Cleo (ag_imxsagd9cj) is at (52,38), on the grass just south of Town Hall. His status is "walking", his activity "Walking to Cleo's desk", and he has no assignment. He has been there since 18:31Z. His desk is at (38,50) and can be reached on the current map (grass, then the Prod door at 38,45). Placement, roads and the map were not the problem.
- **Cause: a restart in the middle of a walk.** His facilitate session ended at 18:31:17.76Z (event 61285), which started his walk home from the Town Hall meeting room. The 8898e8b redeploy restarted the server 1 s later, at 18:31:18.8Z (event 61291).
  - The walk itself is kept only in server memory, but the "walking" status is saved to the database. So after the restart nothing was left to finish the walk.
  - Nothing sends him home afterwards either. `stayReason` treats status "walking" as a reason to stay put, and the walk-home tick only picks up idle bodies. Any redeploy that lands while someone is walking can leave them stuck the same way.
- **Fix (8ffc906):**
  - The startup `reconcile` (which already resets a stale "working" status) now also resets "walking" with no walk in progress to idle, or to working if the agent still has a running session. The runtime tick then walks idle bodies home within about 5 s.
  - `Movement.go` no longer puts back a stale "walking" status when the agent arrives.
  - Typecheck is clean; core tests 496/496 and runtime tests 154/154 pass.
- **No data repair needed:** the next server boot runs reconcile, which fixes Cleo's record.
- **What Mitchell would see:** once 8ffc906 is live, Cleo walks from in front of Town Hall to his desk in Prod within seconds of the restart and shows as idle.
- **Not yet verified:** that 8ffc906 is live and Cleo is at (38,50). I've parked this report and will check both when the deploy lands.

## What I need from you
Nothing needed.
