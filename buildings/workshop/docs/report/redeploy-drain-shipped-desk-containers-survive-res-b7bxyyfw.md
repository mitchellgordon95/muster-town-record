---
id: "dc_hfb7bxyyfw"
type: "report"
state: "building"
title: "Redeploy drain shipped; desk containers survive restarts (orphan sessions now killed)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T16:53:02.128Z"
sessionId: "se_yg10u98vha"
assignmentId: "as_vmflxy4x8c"
costUsd: 0.7530328999999998
tokens: 1096962
turns: 26
createdAt: "2026-10-20T16:46:11.515Z"
updatedAt: "2026-10-20T16:53:02.128Z"
---
## What I did
Drain-then-restart was already on main from my last session (280d204). I checked by reading the code whether desk containers survive a server restart. They do, and that exposed a bug, which I fixed in 6a787e9, pushed straight to main. Then I triggered the redeploy.

## Findings
- **Drain (280d204):** a redeploy stops new work sessions from starting and polls every 5 s, for up to 30 min, until running sessions end. Then it exits 75 and `serve.sh` restarts the server. On timeout it restarts anyway and names the sessions it cut off.
- **Desk containers survive a restart.** They are started with `docker run -d … sleep infinity`, without `--rm`, and nothing removes them when the server exits. Only a dismissal or a redeploy with image=true removes them. Home volumes are always kept.
- **Bug: a session cut off by the drain timeout kept running in its container.** On timeout the redeploy calls `process.exit(75)`, which skips `runtime.stop()`, so the `pkill` inside the container never ran. The `docker exec`'d `agent-town-desk run` therefore kept going. Meanwhile startup reconcile put the same assignment back in the queue, so two sessions could work in the same checkout at once.
- **Fix (6a787e9):** at startup, the server now kills the leftover process for each orphaned docker session inside its container. It uses `docker exec <desk> pkill -TERM -f "agent-town-desk run --session <id>"`. That only matches the old session id, so the new session for the re-queued assignment is safe. New tests cover the kill command and the startup step.
- **Checks:** `npm run typecheck` is clean and all tests pass (runtime 43/43; full suite all green).
- **Not checked live:** my sandbox has no docker. Two things rest on reading the code and on Docker's documented behaviour: that the containers survive, and that a `docker exec` process outlives its client.
- **Redeploy:** started. It will drain until this session ends.

## What I need from you
Nothing needed.
