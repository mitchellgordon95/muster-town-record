---
id: "dc_tji5kkikuw"
type: "report"
state: "building"
title: "Stress step 1, part 2: the viewer ceiling is found (1200 sure, 1600 marginal, 2000 fails) and it is network-path throughput at ~20–25 MB/s, not the server loop or memory; agent ramps, Bottleneck sections and destroy parked for the waiting redeploy"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_jea12u6sal","dc_3e1z30jost","dc_fti3ikjkwj","dc_ckrrf0c0cb","dc_x4twxh1a8o"],"urls":["https://muster.town/api/health","https://muster-town-stress.fly.dev/api/health"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: viewer ceiling and Bottleneck 1 evidence are in dc_jea12u6sal. The remaining work (agent ramps twice, Bottleneck 1 and 2 sections, destroy + fly apps list clean) already resumed as as_74lmibldf8 on the redeploy, so no new assignment; a \"continue\" here would duplicate it. Keep part 3 under 2 M tokens so the 100% checkpoint lands with headroom."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T20:28:58.868Z"
sessionId: "se_27pnjujmbs"
assignmentId: "as_k4gvm1bs00"
costUsd: 3.4633058999999995
tokens: 42840
turns: 37
createdAt: "2026-10-26T19:53:16.908Z"
updatedAt: "2026-10-26T20:28:58.868Z"
---
## What I did
Verified 726df71 live on muster.town (health commit, merge-base ok). Started the throwaway, ran viewer run 3 (1600/2000/2400, 13 walkers, 3 client procs) and run 4 (rerun 1600/1800/2000) with a live-side health poller and a desk-side network counter sampler; checked Fly's service concurrency config, Fly's own check status, and tried Fly Prometheus (401 for FLY_STRESS_TOKEN). Filed both runs in [dc_jea12u6sal](../../note/2026-10/2026-10-26-stress-test-runs-3-and-4-viewer-ramp-1600-2400-and-a12u6sal.md) (files 2026-10-26T19-41-53 and 19-47-32 in ~/.muster-stress/results). A redeploy interrupted before the agent ramps, so I stopped the throwaway (not destroyed) and parked the rest. No code changes; nothing of mine needs to go live.

## Findings
- **Ceiling (viewers, live-scale bodies):** 1200 passed twice (run 2); **1600 passed once** (run 3: 26 frames/s/client, 12.8 kB/s/client ≈ 20.5 MB/s aggregate, health p95 180 ms) **and failed once** (run 4: 6 of 17 health probes timed out at 5 s); **2000 failed** (run 3: 7 of 13 probes timed out, health p95 2486 ms, frames/client collapsed to 5.8 /s). 2400 never ran.
- **Bottleneck 1 (two runs + files): throughput on the network path, ~20–25 MB/s (160–200 Mbit/s) of WebSocket egress.** In every failing step the server's own lagMs max was 192–203 ms and RSS 162–166 MB (far from limits), 0 drops, 0 errors, client loop p99 ≤ 16 ms, while the desk's receive rate ran at ~24 MB/s for ~30 s and then fell to ~3 MB/s with the sockets still open. Which end caps it (throwaway Machine/Fly proxy vs the desk Machine's ingress, both Fly shared-cpu) is not settled: the desk's outbound internet is filtered so no outside bandwidth test, and Fly Prometheus refused the token. Service concurrency is null (Fly default, same as live), so not a configured connection limit.
- **Bottleneck 2 candidate** (to be written with the agent runs): the per-socket fanout in ws.ts, from lagMs growing linearly ~0.1 ms per viewer (run 2) to 112 ms p50 at 1600; it would be next once the path is wider.
- **Live side:** https://muster.town/api/health 107 probes 19:41–19:50 UTC, all 200, max 132 ms; no load sent to muster.town.
- **Remaining for part 3:** agent ramp 5→80 twice (agents.mjs), Bottleneck 1 and 2 sections citing runs and files, `throwaway.sh destroy` + `fly apps list` clean. Optional, cheap: a probe loop from Wright's VPS during one 1600 step would settle which end caps the path.
- Grant spend ~7.9 M / 10 M; this session ≈ 0.15 M.

## What I need from you
Nothing needed.
