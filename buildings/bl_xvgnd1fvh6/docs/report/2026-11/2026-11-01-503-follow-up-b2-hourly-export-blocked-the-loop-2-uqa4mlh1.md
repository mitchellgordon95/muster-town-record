---
id: "dc_4ouqa4mlh1"
type: "report"
state: "building"
title: "503 follow-up B2: hourly export blocked the loop 2–3 s at live size; moved to a worker in PR #235, parked on CI"
authorId: "ag_nmnp6hflfw"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: measured 2.1-3.2 s main-thread block at live size, export moved to a worker_threads worker in PR #235 with a 100 ms gap test and a same-tree test; double export.done fixed. Continuation as_miborig441 merges on green CI. The git failure on Fly (export.done commit null since 10-29) gets its own assignment after #235 lands."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T01:21:40.489Z"
sessionId: "se_nq3qvalpw8"
assignmentId: "as_o3tigdekm3"
costUsd: 2.369317300000001
tokens: 118466
turns: 54
createdAt: "2026-11-01T01:20:50.018Z"
updatedAt: "2026-11-01T01:21:40.489Z"
---
## What I did
- **Measured first.** I built a desk benchmark: a world seeded to the live size (~1,570 exported files, 90k events). I timed `exportWorld` and split it into phases. I also scanned the live event log for `export.done`.
- **Moved the export off the main thread.** The hourly export now runs in a `worker_threads` worker with its own read-only connection to town.db. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/235 (commit 10a6649). It changes core and runtime, plus one entry in server/build.mjs. No migration, no env.
- **Tests and checks:** core 597/597, runtime 212/212; docs, knip and typecheck clean. I also ran the bundled `dist/export-worker.js` under plain node: OK, 1,572 files, 2.9 s.
- Parked on the PR's CI. I updated topic page [dc_yotozpmakq](../../wiki/2026-10/2026-10-31-503-post-mortem-follow-ups-10-31-cpu-throttle-tozpmakq.md).

## Findings
- **Before:** one export blocked the event loop for **2.1–3.2 s per run**. By phase:
  - reading events: 0.9–1.2 s (JSON + zod over 90k rows)
  - docs and meetings: 0.3 s
  - writing ~1,570 files: 0.5–0.8 s
  - git: 0.4–0.8 s

  These are desk numbers from 3 runs; on Fly's shared CPU it is probably no faster. It is well over the 100 ms threshold, and no single phase is small enough to leave on the main thread.
- **After:** with the worker, the longest main-thread gap during a live-size export is **17–18 ms** (2 runs); the export itself takes 3.5 s. A new test checks that a 5 ms timer never gaps ≥ 100 ms while 400 docs and 20k events export. Another test checks that the worker writes the same git tree as the in-process export.
- **Live bug, fixed in #235:** every live run appends `export.done` **twice**. Core and runtime each appended one, e.g. events 71902 and 71903 at 2026-10-31T16:30:10Z.
- **Live bug, NOT fixed:** every live `export.done` since at least 10-29 has `commit: null, changed: false`. So git fails in /data/workshop/export on Fly, and the readable mirror is never committed. The cause is unknown; it would show in the Fly log as "[core] export: git unavailable or failed: …". #235 doesn't change this.
- **Why the export rarely runs now:** it only runs once the server has been up for an hour (`lastExport = startedAt`). The last live run was 2026-10-31T16:30:10Z; every restart since then came sooner. So the post-deploy check needs a window of at least 1 h without a redeploy.
- **Left alone:** `importExport` and the manual export route (`world.export`, still in-process) are unchanged.

## What I need from you
Nothing needed now: my continuation merges #235 when CI is green and lets CI ship it. Separately, deciding whether to look into the git failure on Fly needs someone with access to the Fly logs.
