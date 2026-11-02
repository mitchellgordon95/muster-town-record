---
id: "dc_msbpaawbrs"
type: "report"
state: "building"
title: "Stress test step 0 done: health `load` live-bound (ff0f088), throwaway muster-town-stress built and ramped to 400 viewers with no failure signal; next session finds the ceiling and runs the agent ramp"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_x4twxh1a8o","dc_5mxgn9gj16","dc_fti3ikjkwj"],"urls":["https://github.com/mitchellgordon95/agent-town/commit/ff0f088bc720e347254fee352de48156eae0eae5","https://muster-town-stress.fly.dev/api/health"]}
tags: []
verdict: "continue"
decision: "redirect"
decisionNote: "Stress test, step 1 (grant gr_wqnunw5yd8, key result kr_z9lcfnvt94, plan dc_x4twxh1a8o; method on wiki pages \"Stress harness\" and \"Stress-test grant\"). First confirm ff0f088 and f48e69a are live on muster.town (/api/health commit, merge-base) and that health shows load: {lagMs, rssMb, wsClients}. Then `throwaway.sh start` muster-town-stress and: (1) viewer ramp 400/600/800/1200 with live-scale bodies (13+ walkers, or seed to match live's 13 agents / 26 KB snapshot); if the desk's single Node process saturates first, split clients across processes and say so; stop at the first failure signal per the abort rule and record the ceiling line. (2) agent ramp 5/10/20/40/80 with agents.mjs. (3) Run both ramps a second time so Bottleneck 1 and 2 each cite two runs and a file. One row per step in ~/.muster-stress/results and a results doc in the cabinet. Never touch muster.town with load; check https://muster.town/api/health stayed ok through every window. Leave the throwaway stopped (not destroyed) unless both ramps and both reruns are complete, in which case `throwaway.sh destroy` and confirm `fly apps list` has no muster-town-stress. Budget this session: under 2 M tokens; the grant is at its 50% checkpoint, so this starts when Mitchell continues it."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T18:41:54.875Z"
sessionId: "se_65nujs4rvr"
assignmentId: "as_ruei242ovd"
costUsd: 7.241843349999998
tokens: 218450
turns: 75
createdAt: "2026-10-26T18:32:23.217Z"
updatedAt: "2026-10-26T18:41:54.875Z"
---
## What I did
- Pushed **ff0f088** to main (Prod standing rule; branch `agent/cleo/stress-test-step-0-build-the-throwaway-s` pushed too, no PR): `GET /api/health` gains read-only `load: {lagMs, rssMb, wsClients}` (packages/server/src/load.ts: p99 event-loop delay over the last 10 s, RSS in MiB, open /ws sockets; test in live.test.ts), the only production change. Typecheck and the server suite pass. Follow-up **f48e69a** adds `stop|start` to the throwaway script. I have no `town.redeploy` permission; CI ships green main to prod and a redeploy is already waiting on this session: **ff0f088 and f48e69a should be live** next time (check with `git merge-base --is-ancestor`).
- `deploy/fly/throwaway.sh [create|status|admin-token|stop|start|destroy]`: app `muster-town-stress`, same Dockerfile built from GitHub main (build.sh now takes REPO_URL/BRANCH and extra `fly deploy` flags, and scrubs the clone token from the baked remote), same size and region, 10 GB volume, only secret a fresh random data key, no Claude/GitHub/Fly tokens, desks pointed at an absent docker backend. `scripts/stress/viewers.mjs` (WS ramp 10→400 with walking bodies) and `scripts/stress/agents.mjs` (visitors 5→80 over /mcp), shared `lib.mjs`; both exit 2 on a `muster.town` host before any request (checked). Both ramps verified first on a scratch local town. deploy/README.md "Throwaway for load tests", docs/architecture.md, docs/log.md updated.
- FLY_STRESS_TOKEN **does** arrive on the desk. Ran `throwaway.sh create`: app, volume, key, remote build and deploy took 2.5 min; health answered on ff0f088 at 18:24 UTC; admin token fetched over `fly ssh`. Ran the first viewer ramp; results filed as [dc_fti3ikjkwj](../../note/2026-10/2026-10-26-stress-test-run-1-viewer-ramp-10-400-on-the-throwa-i3ikjkwj.md). Machine stopped afterwards (volume keeps the state; `throwaway.sh start` wakes it).

## Findings
- **Run 1 (viewers, 60 s per step, 8 walkers), all passed, no ceiling yet:**

| viewers | snapshot p95 ms | frames/s/client | event lag p95 ms | health p95 ms | server lagMs max | rss MB | drops |
|---|---|---|---|---|---|---|---|
| 10 | 65 | 19.6 | 1 | 13 | 4 | 148 | 0 |
| 50 | 24 | 19.6 | 5 | 7 | 5 | 150 | 0 |
| 100 | 19 | 18.8 | 11 | 5 | 5 | 150 | 0 |
| 200 | 33 | 19.8 | 20 | 10 | 15 | 153 | 0 |
| 400 | 35 | 20.3 | 36 | 38 | 44 | 155 | 0 |

- The metric that moves is event-loop lag (4 → 44 ms p99) and event delivery lag, with RSS flat: consistent with the per-client stringify fanout (ws.ts) as bottleneck candidate 1. Linear extrapolation says the 2 s line is well past 400, but the throwaway's seed is smaller than live (6 agents, 16.5 KB snapshot vs 13 and 26 KB), so the next ramp runs 400/600/800/1200 with live-scale bodies.
- **The token Mitchell stored is org-wide**, not scoped to muster-town-stress (`fly tokens debug`: mask rwcdC on the whole personal org; it lists muster-town and muster-desks). The script hard-codes the app and refuses the other two, and the token never goes on the throwaway, but it should be re-scoped now that the app exists.
- Grant spend this session: this report's tokens, well under the 2.5 M budget. Fly: the throwaway Machine costs ~$0.02/h running (stopped now), the volume $1.50/month.
- Parked assignment as_iv8fk97gf8 (22:00 UTC) is moot: the grant is filed and funded; report and stop when it fires.

## What I need from you
Replace Town Hall secret FLY_STRESS_TOKEN with an app-scoped one now that the app exists: `fly tokens create deploy -a muster-town-stress` (the current one can touch muster-town and muster-desks).
