---
id: "dc_8mtuqtu51r"
type: "report"
state: "building"
title: "503 follow-up C: 97911e8 live with #225 keys; \"build server\" step shows from the next redeploy"
authorId: "ag_6cjlpgny6a"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. 97911e8 (#230 + #225) live via CI promote; continuation as_6pquvsdieq checks the \"build server\" event on the next deploy. Image deploy already asked for in outbox dc_lyjnyeev9f. Lesson kept: let CI ship merges; manual redeploy only for an image deploy or a no-commit restart. CI debounce veto goes in the next rollup's \"Your call\"."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T00:31:24.770Z"
sessionId: "se_akzf12msq8"
assignmentId: "as_an0yn18eop"
costUsd: 0.5114481000000001
tokens: 25572
turns: 10
createdAt: "2026-11-01T00:31:10.018Z"
updatedAt: "2026-11-01T00:31:24.770Z"
---
## What I did
- Read /api/health and /api/events (redeploy events 89629–89752).
- Rewrote topic page [dc_eka5xluv6o](../../wiki/2026-11/2026-11-01-prebuilt-server-and-ci-redeploy-coalescing-a5xluv6o.md).

## Findings
- **97911e8 is live** (PR #230 and #225): health.commit is 97911e8 and startedAt is 00:30:18Z. CI requested the redeploy at 00:30:06Z, and the restart took 2.9 s (restarting → finished). #225's keys are present: `figuresAt` (0.6 s old when read), `load.tick` with per-phase timings, and all the old keys. `monitor.alerts` is [] and `backup.error` is null.
- **The "build server … ok" step wasn't in this run, as expected.** The old process (c3a49e3) runs a redeploy using its own runtime/redeploy.ts, which doesn't have the step. The first redeploy started from 97911e8 or later will show it. I'm parked on the next deploy to confirm that with one event check.
- **My two manual redeploys were wasted restarts.** `redeploy` pulls `prod`, and only CI's promote job moves `prod`, after main goes green. So both manual redeploys (00:13:27Z and 00:14:55Z) pulled 0 commits and restarted the town for nothing. Each one also reset #230's 15-min debounce, which held CI's real ship until 00:30. Rule from now on: after a merge, let CI ship it, and use `redeploy` only for an image deploy or a redeploy without a new commit. This is on the topic page.
- **The fast boot still needs the town image deploy** (outbox [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md)). Until then the entrypoint runs tsx.

## What I need from you
Run `deploy/fly/build.sh` once (outbox [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md)). PR #230's CI change is town-wide (no redeploy for docs-only changes, at most one CI restart per 15 min); veto it in the rollup if you don't want that.
