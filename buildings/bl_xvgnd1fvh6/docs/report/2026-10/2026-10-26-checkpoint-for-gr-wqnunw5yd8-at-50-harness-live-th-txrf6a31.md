---
id: "dc_fstxrf6a31"
type: "report"
state: "building"
title: "Checkpoint for gr_wqnunw5yd8 at 50%: harness live, throwaway built, viewers 10→400 passed with no ceiling yet; key result on-track, continue the grant"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_msbpaawbrs"],"urls":["https://muster.town/api/health","https://github.com/mitchellgordon95/agent-town/commit/ff0f088bc720e347254fee352de48156eae0eae5"]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T19:00:24.241Z"
sessionId: "se_u6c9uef2n2"
assignmentId: "as_zgc25mardt"
costUsd: 1.2403003499999998
tokens: 13893
turns: 12
createdAt: "2026-10-26T18:44:33.286Z"
updatedAt: "2026-10-26T19:00:24.241Z"
---
## Shipped
- **ff0f088 + f48e69a on main, live on muster.town** (verified 18:43 UTC: `GET https://muster.town/api/health` reports commit f48e69a and `load: {lagMs: 1, rssMb: 181, wsClients: 0}`). The only production change is that read-only `load` field; the rest is `deploy/fly/throwaway.sh` and `scripts/stress/{lib,viewers,agents}.mjs` (both scripts exit 2 on any muster.town host before sending a request).
- **Throwaway app muster-town-stress** exists (Fly shared-cpu-2x / 2 GB, iad, same Dockerfile from main at ff0f088, fresh seed, no live data or secrets). Machine stopped between sessions (`fly apps list` shows it suspended); cost ~$0.02/h while running, $1.50/month for the volume.
- **Run 1, viewer ramp** (results note [dc_fti3ikjkwj](../../note/2026-10/2026-10-26-stress-test-run-1-viewer-ramp-10-400-on-the-throwa-i3ikjkwj.md); raw rows in `~/.muster-stress/results/2026-10-26T18-24-34-viewers.md` on my desk), 60 s per step, 8 walking visitors:

| viewers | snapshot p95 ms | frames/s/client | event lag p95 ms | health p95 ms | server lagMs max | RSS MB | drops | result |
|---|---|---|---|---|---|---|---|---|
| 10 | 65 | 19.6 | 1 | 13 | 4 | 148 | 0 | pass |
| 25 | 19 | 18.7 | 2 | 7 | 2 | 149 | 0 | pass |
| 50 | 24 | 19.6 | 5 | 7 | 5 | 150 | 0 | pass |
| 100 | 19 | 18.8 | 11 | 5 | 5 | 150 | 0 | pass |
| 200 | 33 | 19.8 | 20 | 10 | 15 | 153 | 0 | pass |
| 400 | 35 | 20.3 | 36 | 38 | 44 | 155 | 0 | pass |

Ceiling (viewers): not reached at 400; no failure signal (abort rule: health p95 > 2 s, RSS > 1.6 GB, or 1013 drops). muster.town health stayed ok through the window. No code changes this session; the redeploy waiting on my session end should put main head 6988a43 live.

## Decided
- [dc_msbpaawbrs](2026-10-26-stress-test-step-0-done-health-load-live-bound-ff0-bpaawbrs.md) (step 0 report): **redirect** into step 1 (as_w6hqd4i59e, held until you continue the grant): viewer ramp 400/600/800/1200 with live-scale bodies, agent ramp 5→80, both ramps a second time, Bottleneck 1 and 2 sections each citing two runs and a file, then destroy the throwaway. Budget under 2 M tokens.
- This checkpoint: `checkpoint_grant` filed with the key result **on-track**.

## Key results
- **kr_z9lcfnvt94 — on-track.** How to check: Prod's filing cabinet has the checkpoint report with one row per ramp step, a ceiling line per load, Bottleneck 1 and 2 sections; scripts/stress/ on main; throwaway deleted at the end; muster.town health ok throughout.
- What the testing plan showed so far: harness on main and reproducible against the throwaway (yes, run 1 rows above); ramp steps and failure signals reported (viewer steps yes, no ceiling yet; agent ramp not run); two bottlenecks reproduced twice (not yet; candidate 1 from run 1 is the per-client `JSON.stringify` fanout in `packages/server/src/ws.ts`, where event-loop lag grows 4 → 44 ms while RSS stays flat); live town never loaded (yes: harness refuses muster.town, live health ok); throwaway gone and live health exposes load read-only (load yes; throwaway still exists, stopped, because the ramps are not finished).
- **Spend: 6,553,512 / 10,000,000 tokens** (nearly all of it step 0's session: building the harness and the throwaway plus the first ramp). Step 1 is scoped under 2 M, leaving margin for the reruns.

## Needs from Mitchell
1. **Continue the grant** (gr_wqnunw5yd8) so step 1 (as_w6hqd4i59e) can run: the ceiling, the agent ramp, the two bottlenecks with two runs each, and the throwaway's destruction. Cutting now leaves the KR without a ceiling or bottlenecks; the harness and the throwaway are reusable either way.
2. **Re-scope FLY_STRESS_TOKEN** now that the app exists: `fly tokens create deploy -a muster-town-stress` and replace the Town Hall secret. The current token is org-wide (it can touch muster-town and muster-desks); the script refuses those apps, but an app-scoped token removes the risk entirely.
