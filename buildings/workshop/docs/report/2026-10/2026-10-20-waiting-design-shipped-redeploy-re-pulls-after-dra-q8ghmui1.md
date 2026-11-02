---
id: "dc_b6q8ghmui1"
type: "report"
state: "building"
title: "Waiting design shipped: redeploy re-pulls after drain + live sha (P0), assignments wait on dependencies (P1), agents park their own work and resume automatically (P2)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T20:33:34.409Z"
sessionId: "se_7hoah7r3pt"
assignmentId: "as_hhv7qzp2sk"
costUsd: 3.2400517
tokens: 244946
turns: 72
createdAt: "2026-10-20T20:15:03.258Z"
updatedAt: "2026-10-20T20:33:34.409Z"
---
## What I did
Mitchell approved the whole design in [dc_0sbtispjk3](../../article/2026-10/2026-10-20-design-how-agents-wait-on-in-progress-work-and-pic-btispjk3.md), including automatic resume for P2, so I built all three phases. Both commits are pushed straight to main: **adeb0e9** (P0) and **14f83c4** (P1+P2). `npm run typecheck` is clean and all test suites pass: core 165, runtime 56, server 53, plus the rest. I then requested a redeploy. It pulled both commits and is draining until this session ends. Since the running server is still on the old code, this restart is the one that makes it all live.

## Findings
**P0: redeploys no longer drop commits pushed during the drain** (`runtime/redeploy.ts`)
- **Second pull:** after the drain, the redeploy pulls again. If HEAD moved, it reruns install (only if the lockfile changed), the web build and the image. If that pull fails, it restarts with the build it already had.
- **Joining a run:** a request while a redeploy is running now joins it and returns `{queued:true}`, where before it was refused. A request that asks for an image turns the image build on. A request that arrives after the final pull is saved in the done-file, and the restarted server runs it 10 s after booting.
- **Live commit:** `/api/health` now returns `commit`, the sha the server started from. The "Redeploy finished … at <sha7>" event carries `head`.
- **World rules:** a new line says agents can't wait inside a session, explains how to check whether a change is live, and tells them to park instead.

**P1: assignments that wait** (`core/waits.ts`, migration 020)
- **Conditions:** `Assignment.waitFor` can be one of:
  - `{deploy: sha}`: the live commit contains it.
  - `{deploy: "next"}`: the server restarted after the assignment was made.
  - `{assignment: id}`
  - `{decision: reportId}`
  - `{after: iso}`: at most 24 h ahead.
- **Where it's set:** `assign`, `POST /agents/:id/work`, review continue/redirect, and meeting `decide`, so "after the redeploy" can now be `{deploy:"next"}`.
- **What the scheduler does:** it skips waiting assignments, and the runtime tick clears a wait once it's met, with an "unblocked" event. A wait still unmet after 24 h is cancelled into the in-tray, and Continue there re-queues it without the wait. Start-next overrides a wait. The queue row in the Agent panel shows "waiting: …".

**P2: parking your own work**
- **How:** `submit_report` takes `resumeWhen` and `next`. The report lands in the in-tray tagged `parked`, and a continuation is queued at the front. It **resumes by itself** once its condition holds.
- **In-tray actions:** Approve leaves it parked, Continue resumes it now, and Redirect or Stop cancel it.
- **Limits:** at most 3 parks in a row, and the same 24 h expiry applies.

**Not done:** auto-review buildings can also park. My design leaned against that, but your reply didn't restrict it, so the 3-park cap is the only guard there. The live check of the redeploy happens after this session ends, so I haven't seen the restarted server myself. To confirm, see the "Redeploy finished … at 14f83c4" event, or `GET /api/health`, which should show `commit` = 14f83c4….

## What I need from you
Nothing needed.
