---
id: "dc_qs6y1j2eh6"
type: "report"
state: "building"
title: "Stress step 1, part 3 done: scripted agents pass to 160 with no ceiling (two runs), Bottleneck 1 (network path ~20–25 MB/s) and 2 (per-socket JSON fanout in ws.ts) written up in dc_dzky22ajws, throwaway destroyed and fly apps list clean; grant step 1 complete"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_dzky22ajws","dc_jea12u6sal","dc_3e1z30jost","dc_fti3ikjkwj","dc_x4twxh1a8o"],"urls":["https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 1 of gr_wqnunw5yd8 complete: both ramps and both reruns done, bottlenecks written up, throwaway destroyed. Filing the checkpoint as claimed in this session; FLY_STRESS_TOKEN revoke/re-scope goes to Mitchell in the rollup."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T21:04:41.806Z"
sessionId: "se_9ra6kp39d5"
assignmentId: "as_74lmibldf8"
costUsd: 2.1877086500000003
tokens: 24352
turns: 19
createdAt: "2026-10-26T20:43:14.892Z"
updatedAt: "2026-10-26T21:04:41.806Z"
---
## What I did
Started the throwaway muster-town-stress (ff0f088), ran the agent ramp twice with `scripts/stress/agents.mjs` (run 5: 5/10/20/40/80 agents, 60 s holds; run 6: 40/80/160, 40 s holds because a redeploy was waiting on my session), polled https://muster.town/api/health every 5 s throughout, wrote the results doc with the Bottleneck 1 and 2 sections ([dc_dzky22ajws](../../note/2026-10/2026-10-26-stress-test-runs-5-and-6-agent-ramp-5-80-and-rerun-ky22ajws.md)), then `throwaway.sh destroy` and confirmed `fly apps list` shows only muster-desks and muster-town. No code changed; nothing to push or deploy from me (the waiting redeploy is someone else's; live was already bdc44f0 = main at 20:29).

## Findings
- **Scripted agents: no ceiling to 160 agents / 54 verbs/s** (files 2026-10-26T20-30-13-agents and 20-36-44-agents in ~/.muster-stress/results). At 80 agents: lagMs max 6–10 ms, RSS 158–172 MB, health p95 9 ms; at 160: lagMs max 11 ms, RSS 186 MB, health p95 14 ms, 0 errors. look/say/write/search/inbox stayed ≤ 25 ms p95; `go` p50 2–4 s is the walk itself. Caveat: the throwaway ran no desk sessions (maxRunning 1), so this is the server's MCP verb capacity, not Docker/LLM desk capacity.
- **Viewer ceiling (from parts 1–2, unchanged): 1200 sustained, 1600 marginal (pass once, fail once), 2000 fails**, with 13 moving bodies and a live-scale 23.5 KB snapshot.
- **Bottleneck 1 = network-path throughput, ~20–25 MB/s (160–200 Mbit/s) of WebSocket egress** (runs 3 and 4, [dc_jea12u6sal](../../note/2026-10/2026-10-26-stress-test-runs-3-and-4-viewer-ramp-1600-2400-and-a12u6sal.md)): health probes time out at 5 s and frames per client collapse while the server's own lagMs stays ≤ 203 ms and RSS ≤ 166 MB. Which end caps it (Fly NIC/proxy of the Machine vs the desk's ingress) is not settled.
- **Bottleneck 2 = per-socket JSON.stringify + send fanout in packages/server/src/ws.ts** (`stream()` subscribes each socket's `send` to `world.changes`; N stringifies per change). Evidence runs 2 and 3: server lagMs p50 28 → 77 ms over 400 → 1200 viewers, 112 ms at 1600 (≈ 0.06 ms per viewer, ≈ 40 000 stringify+send per second). Linear extrapolation (not measured) puts ~200 ms loop delay near 2500–3000 viewers once the path is wider. Fix idea: stringify once per change and coalesce moves per tick.
- **Live side:** muster.town answered 114 of 114 probes with HTTP 200, max 131 ms, 20:30–20:40 UTC. No load went to muster.town.
- **Cleanup:** app muster-town-stress (Machine d891167db76778 and volume) destroyed 20:40 UTC; `fly volumes list -a muster-town-stress` → app not found. Both ramps and both reruns are complete, so the grant's step 1 is done; the 100% checkpoint can claim kr_z9lcfnvt94 with the ceilings above.

## What I need from you
Nothing needed. (For the next rollup: FLY_STRESS_TOKEN is org-wide and the throwaway is gone; Mitchell could revoke it or re-scope it.)
