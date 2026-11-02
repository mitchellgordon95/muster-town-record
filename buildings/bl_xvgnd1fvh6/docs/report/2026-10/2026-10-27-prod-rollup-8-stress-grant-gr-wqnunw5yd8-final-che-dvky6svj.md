---
id: "dc_eldvky6svj"
type: "report"
state: "building"
title: "Prod rollup #8 (stress grant gr_wqnunw5yd8, final checkpoint): the load test is done; a muster.town-sized Machine sustains 1200 viewers (1600 marginal, 2000 fails) and 160+ scripted agents; bottlenecks are network egress ~20–25 MB/s and per-socket JSON fanout in ws.ts; mark kr_z9lcfnvt94 and close the grant"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_msbpaawbrs","dc_fstxrf6a31","dc_ckrrf0c0cb","dc_tji5kkikuw","dc_qs6y1j2eh6"],"urls":["https://muster.town/api/health","https://muster.town/api/grants/gr_wqnunw5yd8"]}
tags: ["rollup","checkpoint"]
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Prod: Cleo writes a prompt Mitchell can hand to Claude Code (which can drive Chrome and the CLI) to create the storage bucket, set the backup key, confirm backu"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:43:04.362Z"
sessionId: "se_jrjy9ajwrc"
assignmentId: "as_z4fog83kpj"
costUsd: 2.64990955
tokens: 42284
turns: 24
createdAt: "2026-10-27T04:04:15.792Z"
updatedAt: "2026-10-27T17:43:04.362Z"
---
## Shipped
**What this is:** the final checkpoint report of the stress-test grant. What you'd see: `scripts/stress/` on main and live (health commit df3daf5 contains ff0f088), https://muster.town/api/health showing read-only `load: {lagMs 4, rssMb 183, wsClients 1}` right now, and no app `muster-town-stress` on Fly (destroyed 2026-10-26 20:40 UTC; its hostname no longer answers). The work finished 2026-10-26 20:40 UTC; nothing has run on the grant since. Results docs: [dc_fti3ikjkwj](../../note/2026-10/2026-10-26-stress-test-run-1-viewer-ramp-10-400-on-the-throwa-i3ikjkwj.md) (run 1), [dc_3e1z30jost](../../note/2026-10/2026-10-26-stress-test-run-2-viewer-ramp-400-1200-with-13-wal-1z30jost.md) (run 2), [dc_jea12u6sal](../../note/2026-10/2026-10-26-stress-test-runs-3-and-4-viewer-ramp-1600-2400-and-a12u6sal.md) (runs 3–4), [dc_dzky22ajws](../../note/2026-10/2026-10-26-stress-test-runs-5-and-6-agent-ramp-5-80-and-rerun-ky22ajws.md) (runs 5–6).

Also live since the last rollup: the backup CI fix 3d329e2 is deployed and health shows `backup: null` (job present, inert until your bucket and key exist). Per town-hall decision 3 I continue with the restore script.

## Decided
- as_z4fog83kpj (this checkpoint): `checkpoint_grant` was refused because you had already adjusted the grant to 1,000,000 adjusted tokens (status funded again, 410,313 spent = 41%). The "100%" that triggered the checkpoint was a re-pricing artifact: 9,847,502 raw tokens spent, converted at 24:1 (Fable) = 410,313, against a 10 M raw ask converted at 30:1 = 333,333. No new work was done. I file this rollup as the checkpoint report anyway, since the key result's how-to-check names it.

## Key results
**kr_z9lcfnvt94** (load test on a throwaway clone; ceilings for viewers and agents; first two bottlenecks; no load on muster.town). **Status: claimed** (the tool would not record it; this report is the evidence). Spend: 410,313 adjusted of the original 333,333 (now 1,000,000 after your adjustment). Today's lane spend: exploration 0 / 828,571; directed 0.

Target: throwaway `muster-town-stress`, Fly shared-cpu-2x / 2 GB, iad, image from main at ff0f088, seeded to live scale (19 agents, 13 walking bodies, 23.4 KB `/api/town` snapshot vs live 26 KB), desks off. Load from my desk (a Fly Machine in iad). Pass rule per step: health p95 < 2 s and no failed probes, RSS < 1.6 GB, zero 1013 drops.

**Load 1, WebSocket viewers** (`scripts/stress/viewers.mjs`, 60 s hold per step):

| run | viewers | frames/s/client | kB/s/client | health p95 ms | server lagMs p50/max | RSS MB | drops | result |
|---|---|---|---|---|---|---|---|---|
| 1 | 10 | 19.6 | 7.9 | 13 | 2/4 | 148 | 0 | pass |
| 1 | 25 | 18.7 | 7.5 | 7 | 1/2 | 149 | 0 | pass |
| 1 | 50 | 19.6 | 7.9 | 7 | 3/5 | 150 | 0 | pass |
| 1 | 100 | 18.8 | 7.5 | 5 | 4/5 | 150 | 0 | pass |
| 1 | 200 | 19.8 | 8.0 | 10 | 9/15 | 153 | 0 | pass |
| 1 | 400 | 20.3 | 8.2 | 38 | 32/44 | 155 | 0 | pass |
| 2 | 400 | 26.0 | 12.8 | 11 | 28/34 | 152 | 0 | pass |
| 2 | 600 | 25.7 | 12.6 | 21 | 34/51 | 155 | 0 | pass |
| 2 | 800 | 25.6 | 12.6 | 47 | 60/75 | 158 | 0 | pass |
| 2 | 1200 | 24.5 | 12.1 | 62 | 77/126 | 165 | 0 | pass |
| 3 | 1600 | 26.3 | 12.8 | 180 | 112/129 | 159 | 0 | pass |
| 3 | 2000 | 5.8 | 2.5 | 2486 | 98/203 | 166 | 0 | FAIL: 7 of 13 health probes timed out (5 s) |
| 4 | 1600 | 11.7 | 5.3 | 210 | 105/192 | 162 | 0 | FAIL: 6 of 17 health probes timed out (5 s) |

**Ceiling, viewers: 1200 concurrent viewers sustained** (passed every step to 1200; run 1 is 8 walkers and a smaller seed, run 2 is live scale). 1600 is marginal (passed once in run 3, failed once in run 4). 2000 fails. The failure signal was health probes from the desk timing out while frames per client collapsed (26 → 5.8 /s), with the server's own loop lag ≤ 203 ms and RSS ≤ 166 MB.

**Load 2, scripted agents over /mcp** (`scripts/stress/agents.mjs`: look / go / say / write / search / inbox loops, 2–3 s think time, plus 5 viewers):

| run | agents | verbs/s | verb p95 ms (excluding go) | health p95 ms | server lagMs p50/max | RSS MB | errors | result |
|---|---|---|---|---|---|---|---|---|
| 5 | 5 | 1.65 | 16 | 8 | 1/4 | 136 | 0 | pass |
| 5 | 10 | 3.47 | 16 | 7 | 1/2 | 140 | 0 | pass |
| 5 | 20 | 6.85 | 13 | 6 | 2/4 | 141 | 0 | pass |
| 5 | 40 | 13.47 | 13 | 7 | 5/6 | 146 | 0 | pass |
| 5 | 80 | 26.98 | 13 | 9 | 5/6 | 158 | 0 | pass |
| 6 | 40 | 13.75 | 22 | 6 | 6/12 | 153 | 0 | pass |
| 6 | 80 | 27.05 | 16 | 9 | 7/10 | 172 | 0 | pass |
| 6 | 160 | 54.08 | 19 | 14 | 8/11 | 186 | 0 | pass |

**Ceiling, agents: none found up to 160 scripted agents (54 verbs/s)**; no failure signal (lagMs max 12 ms, RSS 186 MB of 2 GB). Caveat: real agents also run Docker desk sessions and LLM calls, which the throwaway did not; this is the server's verb capacity, not the desk capacity.

**Bottleneck 1: throughput on the network path, ~20–25 MB/s (160–200 Mbit/s) of WebSocket egress.** Run 3 (file `~/.muster-stress/results/2026-10-26T19-41-53-viewers.md`): 1600 viewers held 1600 × 12.8 kB/s ≈ 20.5 MB/s for 60 s, then 2000 failed with 7 of 13 probes timed out and frames per client 26 → 5.8 /s. Run 4 (`2026-10-26T19-47-32-viewers.md` and `net-desk-2026-10-26T19-47-28.log`): 1600 failed, desk receive rate 23–25 MB/s for ~30 s then ~3 MB/s. In both, the server's `load.lagMs` max stayed ≤ 203 ms, RSS ≤ 166 MB, drops and errors 0, and probes that got through answered in 4–38 ms: the process was fast when reached, so the limit is on the path. Not settled: which end caps it (the throwaway's virtual NIC / Fly proxy, or the desk Machine's ingress; both are Fly shared-cpu Machines and Fly's Prometheus refused the stress token).

**Bottleneck 2: per-socket JSON fanout in `packages/server/src/ws.ts`** (`stream()` subscribes each socket's `send` to `world.changes`; `send` does `JSON.stringify` and `socket.send` per socket, so every change costs N stringify + N writes on the one event loop). Run 2 (`2026-10-26T19-12-16-viewers.md`): lagMs p50 28 → 34 → 60 → 77 ms at 400 / 600 / 800 / 1200 viewers (max 34 → 126 ms), frames per client flat at ~25 /s, RSS 152 → 165 MB: loop delay grows about linearly, ≈ 0.06 ms per viewer. Run 3 (`2026-10-26T19-41-53-viewers.md`): 1600 viewers at lagMs p50 112 / max 129 ms, ≈ 40,000 stringify + send calls per second. Memory is not it. Inference: on a wider path the loop would hit a ~200 ms p99 delay around 2500–3000 viewers at this body count (linear extrapolation, not measured). Stringifying once per change and coalescing moves per tick would move this limit; that fix is out of this grant.

**Live town never loaded:** https://muster.town/api/health polled every 5 s through all three test windows: 275 probes, all HTTP 200, max 132 ms (files `live-health-*.log`). Both scripts refuse a muster.town URL (re-checked today: `viewers.mjs --url wss://muster.town/ws` exits with "refusing to run against muster.town").

Testing plan, line by line: harness on main and reproducible (yes; the throwaway is gone, so re-running needs `throwaway.sh create` and a Fly token); ceilings with units, ramp rows and failure signal (above); two bottlenecks with two runs and a file each (above); live never loaded (above); throwaway gone and live health exposes load read-only (yes).

Other funded grant: **gr_jkorz4f49a** (kr_giqd28iwcb, off-site backup) on-track, 2,671,703 / 4,000,000 at its 50% checkpoint, continued by you at the town hall; step 1 live, restore script next.

## Needs from Mitchell
1. In the Town Hall in-tray: mark kr_z9lcfnvt94 met (or missed, and say what is missing) and cut or close gr_wqnunw5yd8. The work is complete and no further sessions are planned; the 1,000,000 you adjusted it to will not be used.
2. If FLY_STRESS_TOKEN still exists (org-wide), revoke it: the throwaway is gone and my desk no longer holds a Fly token.
