---
id: "dc_t4sc3cxjk5"
type: "report"
state: "building"
title: "503 follow-up A: PR #225 open (steal alert, health from memory, check timeout 10 s); parked on CI"
authorId: "ag_02aa0vvi1m"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #225 (d62aa6f) built as planned; continuation as_e8xykay8h5 already waits on its CI to merge and redeploy. Note for the merge session: the 10 s check timeout needs an image redeploy, so a plain redeploy leaves it unapplied; say so in the report."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-31T23:36:39.817Z"
sessionId: "se_mrfxk4hj2y"
assignmentId: "as_2bzdo18fp7"
costUsd: 1.3294738000000001
tokens: 66474
turns: 31
createdAt: "2026-10-31T23:36:30.331Z"
updatedAt: "2026-10-31T23:36:39.817Z"
---
## What I did
Built all three parts of follow-up A in one PR: https://github.com/mitchellgordon95/muster-town/pull/225 (head d62aa6f, marked ready for review). Typecheck passes and all server tests pass locally (28 files). I've parked the work until CI finishes. If CI passes, the next session merges it, runs a plain redeploy and checks the live health keys. Topic page: [dc_yotozpmakq](../../wiki/2026-10/2026-10-31-503-post-mortem-follow-ups-10-31-cpu-throttle-tozpmakq.md).

## Findings
- **New `steal` alert** (`packages/server/src/monitor.ts`, `hostStealMetric`):
  - It reads /proc/stat at each 60 s sample and computes steal / (busy + steal) since the previous sample.
  - Yellow above 25 % for 5 min, red above 50 % for 3 min. These are the same hold times as `lag`.
  - A minute with less than 3 s of busy + steal counts as clean, so an idle server can't raise a false alarm.
  - It gives no reading off Linux.
  - The FYI reads `host CPU throttled (steal N%): see deploy/README.md "Slow or 503"`.
  - Wright's pinger already forwards every red key, so a red steal alert reaches Mitchell without any pinger change.
  - Three new tests.
- **`/api/health` answers from memory** (new `health-cache.ts`):
  - `budgets`, `backup`, `desks`, `directory` and `funding` are the only fields that read SQLite. They are now recomputed every 5 s on a timer, and the route serves the cached copy.
  - Every existing key is kept, plus a new `figuresAt` that says when the figures were computed. So nothing changes for the pinger (`ok`, `monitor.alerts`) or the morning check (`backup.*`).
  - New test/health.test.ts: once health has been served, a request makes zero database queries.
  - Tests still compute per request (refresh period 0).
- **Check timeout** in fly.town.toml: 5 s → 10 s, with the reason added to deploy/README.md "Slow or 503". The new value only takes effect at the next image deploy (`deploy/fly/build.sh`). The town's `redeploy` doesn't apply it.
- **No 60 s boot grace added:** the check already has `grace_period = "240s"`, which covers a restart.

## What I need from you
Nothing needed.
