---
id: "dc_258ct4a96c"
type: "wiki"
state: "building"
title: "Stress test: harness and results"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_xvgnd1fvh6"
createdAt: "2026-10-29T03:49:15.176Z"
updatedAt: "2026-11-04T00:43:27.480Z"
---
State on 2026-11-04 (step 4 of gr_n0p3ast5pp in PR #291, opened after the desk's 00:40 UTC test run; CI pending).

**The written path to scale is docs/scaling.md on main** (PR #260 merged as dafe76e, 11-03; linked from deploy/README.md "Prod on Fly.io"). It holds 8 resource rows (WS egress, WS fanout, runtime tick, restarts, db/volume, backup/export, desk slots and bill, RSS), each with ceiling + source, live value, trigger and next fix; the tick table; the fanout before/after table (below); written-only scale-out options; and the capacity triggers for step 3. Update docs/scaling.md, not this page, when a ceiling is re-measured.

**Capacity triggers (step 3 must match):** wsClients ≥ 600 (ceiling 1,200); tick p95 over 100 ticks ≥ 350 ms (limit 500); db ≥ 1,000 MB or volume free < 50 % (10 GB); restarts > 10 in 24 h.

**Step 4, stringify-once (kr_vc8rkafulk): PR #291, commit e087aa62, branch agent/cleo/gr-n0p3ast5pp-step-4-re-queued-without-t.** ws.ts keeps one `world.changes` subscription per server; the per-socket readyState / too-slow checks stay; snapshot and error frames stay per socket; test live.test.ts "stringified once". Desk benchmark (1 vCPU desk, server `MUSTER_TOWN_RUNTIME=off MUSTER_TOWN_DEV=1` on :4399, admin token from `/api/dev/admin-token`, `viewers.mjs --steps 1000 --hold 60 --procs 4 --walkers 8`, three holds each way, medians): ms per change at 1,000 sockets 25.2 → 20.7 wall (12.7 → 10.5 CPU, −17/18 %); lag p50 111 → 85 ms (−23 %); 6.9 kB/s per client; 0 drops. Just under the plan's 20 % line on the per-change figure, over it on lag; kept (also removes code). Rest of the fan-out is the `ws` framing + write per socket (~10 µs each); pre-framing (`Sender.frame`, private `_socket` write) is the only further cut and is not worth its risk until row 2 fires. Scripts: `~/ws-bench/server.sh <tag>` and `~/ws-bench/holds.sh <tag>` on Cleo's desk; raw logs /tmp/ws-bench (not persistent). Desk gotchas: `npm ci` first (stale zod 3 in node_modules), `pkill -f tsx` kills the calling shell too (run it alone), the stress lib caches walker tokens per host in ~/.muster-stress/visitors-<host>.json (delete between fresh data dirs).

**Stress test: done.** kr_z9lcfnvt94 MET (Mitchell, 10-27); grant gr_wqnunw5yd8 closed 10-27 (452,597 of 1,000,000). Close rollup #12 [dc_uypv19h0qe](../../report/2026-10/2026-10-27-prod-rollup-12-close-report-for-gr-wqnunw5yd8-the-pv19h0qe.md); checkpoint rollup #8 [dc_eldvky6svj](../../report/2026-10/2026-10-27-prod-rollup-8-stress-grant-gr-wqnunw5yd8-final-che-dvky6svj.md); results [dc_fti3ikjkwj](../../note/2026-10/2026-10-26-stress-test-run-1-viewer-ramp-10-400-on-the-throwa-i3ikjkwj.md), [dc_3e1z30jost](../../note/2026-10/2026-10-26-stress-test-run-2-viewer-ramp-400-1200-with-13-wal-1z30jost.md), [dc_jea12u6sal](../../note/2026-10/2026-10-26-stress-test-runs-3-and-4-viewer-ramp-1600-2400-and-a12u6sal.md), [dc_dzky22ajws](../../note/2026-10/2026-10-26-stress-test-runs-5-and-6-agent-ramp-5-80-and-rerun-ky22ajws.md). FLY_STRESS_TOKEN revoked 10-27; throwaway destroyed 10-26.

**Rule (Mitchell): load never goes to muster.town.** Both stress scripts exit 2 on a muster.town host.

**Ceilings** (clone of the Machine as shared-cpu-2x / 2 GB; live is performance-1x since 10-31, not re-measured): viewers 1,200 sustained / 1,600 marginal / 2,000 fail; scripted agents no ceiling up to 160. Bottleneck 1: WS egress ~20–25 MB/s. Bottleneck 2: per-socket fan-out in ws.ts (stringify part removed by step 4).

**Tick benchmark** ([dc_er6dxw6kil](../../note/2026-11/2026-11-02-tick-benchmark-1-2-4-gr-n0p3ast5pp-step-1-6dxw6kil.md)): desk p95 163 / 473 / 1,841 ms at 1× / 2× / 4×; live crosses 500 ms at ~1.5×. ~70% of tick CPU is Bank.expectedSession (proposal gr_db6ofyd0yf, page [dc_ur1qzaxafp](../2026-11/2026-11-03-runtime-tick-cost-gr-db6ofyd0yf-1qzaxafp.md)). Script `~/scaling-bench/bench.mts` (Cleo 1's desk).

**Harness on main** (ff0f088, f48e69a, 726df71): scripts/stress/viewers.mjs, agents.mjs, lib.mjs (refuseLive, abort rules). Throwaway: `FLY_API_TOKEN=<org token> deploy/fly/throwaway.sh [create|start|stop|status|admin-token|destroy]`, needs a new org Fly token from Mitchell.
