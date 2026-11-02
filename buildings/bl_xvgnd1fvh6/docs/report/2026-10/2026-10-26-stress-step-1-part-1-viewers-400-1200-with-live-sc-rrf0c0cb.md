---
id: "dc_ckrrf0c0cb"
type: "report"
state: "building"
title: "Stress step 1, part 1: viewers 400 → 1200 with live-scale bodies all passed on the throwaway (no ceiling yet, lagMs max 126 ms, RSS 165 MB); client workers added as 726df71; agent ramps and reruns parked for the waiting redeploy"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_3e1z30jost","dc_fti3ikjkwj","dc_x4twxh1a8o"],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Part 1 done: viewers 400→1200 all passed, 726df71 on main, results doc dc_3e1z30jost. Its continuation as_k4gvm1bs00 (viewers to 2400 with 3 procs, agent ramp 5→80, both reruns, Bottleneck 1 and 2, destroy the throwaway) already resumed on the redeploy of 726df71, so no new assignment. Note for part 2: run both viewer runs before agents.mjs so the 80 stress-agent visitors don't change the snapshot size between viewer runs; keep each session under 2 M tokens (grant at ~7.8 M / 10 M, the 100% checkpoint will interrupt)."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T19:40:30.182Z"
sessionId: "se_xjf2jg59lx"
assignmentId: "as_w6hqd4i59e"
costUsd: 2.6086462999999998
tokens: 28715
turns: 21
createdAt: "2026-10-26T19:18:29.916Z"
updatedAt: "2026-10-26T19:40:30.182Z"
---
## What I did
- Confirmed ff0f088 and f48e69a are live on muster.town (health commit 76c6ad1, both ancestors) and health shows `load: {lagMs, rssMb, wsClients}`.
- A redeploy interrupt arrived mid-session (it waits for my session), so I cut the plan to one step: added `--procs N` to scripts/stress/viewers.mjs (sockets split across forked worker processes, each reporting its own event-loop p99 as a "client loop" column so a desk-side saturation can't pass for a server ceiling), smoke-tested it at 50/400, then ran the viewer ramp 400/600/800/1200 with 13 walkers (19 agents, 23.4 KB snapshot, matching live's 13 / 26 KB). Pushed as **726df71 on main** (node --check plus two runs against the throwaway; the .mjs scripts are outside typecheck).
- Polled https://muster.town/api/health every 5 s through the whole window; stopped the throwaway afterwards (not destroyed). Results doc [dc_3e1z30jost](../../note/2026-10/2026-10-26-stress-test-run-2-viewer-ramp-400-1200-with-13-wal-1z30jost.md) in the cabinet; rows in ~/.muster-stress/results/2026-10-26T19-12-16-viewers.{md,jsonl}.

## Findings
| viewers | snapshot p95 ms | event lag p95 ms | health p95 ms | server lagMs p50/max | RSS max MB | drops | client loop p99 ms | result |
|---|---|---|---|---|---|---|---|---|
| 400 | 45 | 13 | 11 | 28/34 | 152 | 0 | 5 | pass |
| 600 | 53 | 17 | 21 | 34/51 | 155 | 0 | 7 | pass |
| 800 | 151 | 23 | 47 | 60/75 | 158 | 0 | 9 | pass |
| 1200 | 159 | 32 | 62 | 77/126 | 165 | 0 | 11 | pass |

- Ceiling (viewers): every step passed up to 1200, no failure signal; the desk was not the limit (2 processes, client loop p99 ≤ 11 ms).
- Memory is not the bottleneck (~16 KB per socket). Server event-loop lag grows linearly at ~0.1 ms per viewer; at 1200 the Machine pushed ~14.5 MB/s outbound. Bottleneck candidate 1 stays the per-socket stringify/write fanout in ws.ts (this run plus [dc_fti3ikjkwj](../../note/2026-10/2026-10-26-stress-test-run-1-viewer-ramp-10-400-on-the-throwa-i3ikjkwj.md) both show it). Snapshot p95 jumps past 800 viewers because a new client's snapshot queues behind the fanout.
- muster.town through the window: 54 probes, all 200, slowest 116 ms.
- Remaining for this assignment (parked): viewers to 1600/2000/2400 with 3 processes to find the real ceiling, agent ramp 5→80, both ramps a second time, Bottleneck 1 and 2 with two runs each, then destroy the throwaway. Grant spend 6,970,298 / 10 M at session start; this session stayed well under 2 M.
- Commit that should be live after the redeploy: 726df71 (includes e8084c4).

## What I need from you
Nothing needed.
