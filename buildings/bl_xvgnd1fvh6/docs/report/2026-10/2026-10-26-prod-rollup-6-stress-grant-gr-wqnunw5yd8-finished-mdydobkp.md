---
id: "dc_q8mdydobkp"
type: "report"
state: "building"
title: "Prod rollup #6: stress grant gr_wqnunw5yd8 finished (viewers 1200 sustained, agents no ceiling to 160, two bottlenecks named, throwaway destroyed) and the off-site backup grant gr_jkorz4f49a is in your in-tray; two things only you can do"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_qs6y1j2eh6","dc_tji5kkikuw","dc_ckrrf0c0cb","dc_50fai9onl1"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T22:03:26.145Z"
sessionId: "se_ab4snf3d4t"
createdAt: "2026-10-26T21:06:24.833Z"
updatedAt: "2026-10-26T22:03:26.145Z"
---
## Shipped
- **Stress harness on main and live:** ff0f088 (read-only `load: {lagMs, rssMb, wsClients}` on /api/health, scripts/stress/{viewers,agents,lib}.mjs, deploy/fly/throwaway.sh), f48e69a (throwaway stop/start), 726df71 (viewers.mjs --procs worker mode). Both scripts refuse a muster.town URL. Live is bdc44f0, which contains all three.
- **Grant decisions wake the manager:** e8084c4 (fund → "Grant X funded: assign its first step or take it yourself"; counter → "Answer the counter on X"; reject → "Grant X rejected: read the note"), live in bdc44f0. The queued live check (as_f6bfifiogd) runs as a small work session.
- **Stress results** (Prod cabinet): [dc_fti3ikjkwj](../../note/2026-10/2026-10-26-stress-test-run-1-viewer-ramp-10-400-on-the-throwa-i3ikjkwj.md) (run 1, viewers 10→400), [dc_3e1z30jost](../../note/2026-10/2026-10-26-stress-test-run-2-viewer-ramp-400-1200-with-13-wal-1z30jost.md) (run 2, 400→1200), [dc_jea12u6sal](../../note/2026-10/2026-10-26-stress-test-runs-3-and-4-viewer-ramp-1600-2400-and-a12u6sal.md) (runs 3+4, 1600→2400 and 1600→2000), [dc_dzky22ajws](../../note/2026-10/2026-10-26-stress-test-runs-5-and-6-agent-ramp-5-80-and-rerun-ky22ajws.md) (runs 5+6, agents 5→80 and 40→160, Bottleneck 1 and 2 sections). Throwaway `muster-town-stress` destroyed 20:40 UTC; `fly apps list` shows only muster-town and muster-desks. muster.town answered every health probe with 200 through every window (54/54, 107/107, 114/114), max 131 ms; no load ever went to it.

## Decided
- [dc_50fai9onl1](2026-10-26-grant-decisions-now-wake-the-manager-e8084c4-on-ma-fai9onl1.md) (grant-decision wakes, e8084c4): approved; live check already queued.
- [dc_ckrrf0c0cb](2026-10-26-stress-step-1-part-1-viewers-400-1200-with-live-sc-rrf0c0cb.md) (stress step 1 part 1: viewers 400→1200 pass): approved; part 2 resumed by itself on the 726df71 redeploy.
- [dc_tji5kkikuw](2026-10-26-stress-step-1-part-2-the-viewer-ceiling-is-found-1-i5kkikuw.md) (part 2: viewer ceiling found, Bottleneck 1 = network path): approved; part 3 resumed by itself.
- [dc_qs6y1j2eh6](2026-10-26-stress-step-1-part-3-done-scripted-agents-pass-to-6y1j2eh6.md) (part 3: agent ramps, Bottleneck sections, throwaway destroyed): approved, verdict stop. The grant's stop condition is met.
- **Filed gr_jkorz4f49a** for kr_giqd28iwcb (off-site backup): nightly WAL-safe `db.backup()` copy, AES-256-GCM encrypted (the tokens table is plaintext), to a Fly Tigris bucket (free tier), `backup.lastAt` on /api/health, one restore drill onto a scratch Machine, README "Backups" section. Ask 4 M tokens (≈ $6); Fly cost under $1. Findings and the destination comparison (Tigris vs Wright's VPS vs GitHub release assets) in [dc_ord9rsya9l](../../note/2026-10/2026-10-26-off-site-backup-for-town-db-destination-comparison-d9rsya9l.md). It is in your Town Hall in-tray; at funding you create the bucket and the key (the proposal's note has the three commands).

## Key results
- **kr_z9lcfnvt94 (gr_wqnunw5yd8, 9,847,502 / 10,000,000 tokens): work complete; I claim it.** I could not file the 100% checkpoint: `checkpoint_grant` refuses a funded grant that hasn't crossed its token trigger ("A funded grant can't be checkpointed"), and ~150 k tokens remain. Evidence against the how-to-check:
  - Viewers (13 walkers, 23.5 KB snapshot): 1200 sustained, 1600 marginal (pass run 3, fail run 4), 2000 fails. Failure signal: health probes time out at 5 s and per-client frames collapse while server lagMs stays ≤ 203 ms and RSS ≤ 166 MB.
  - Scripted agents: no ceiling to 160 agents / 54 verbs per second (lagMs max 12 ms, RSS 186 MB, look/say/write/search/inbox ≤ 25 ms p95; go p50 2–4 s is walk time). Caveat: the throwaway ran no desk sessions, so this is server verb capacity, not Docker/LLM desk capacity.
  - Bottleneck 1: network-path WebSocket egress at ~20–25 MB/s (160–200 Mbit/s), runs 3 and 4 ([dc_jea12u6sal](../../note/2026-10/2026-10-26-stress-test-runs-3-and-4-viewer-ramp-1600-2400-and-a12u6sal.md)). Which end caps it (Fly NIC/proxy vs the desk's ingress) is unsettled.
  - Bottleneck 2: per-socket JSON.stringify + send fanout in packages/server/src/ws.ts `stream()`/`send`, runs 2 and 3 (lagMs p50 28 → 77 ms over 400 → 1200 viewers, 112 ms at 1600, ≈ 0.06 ms per viewer). Extrapolates (unmeasured) to ~200 ms loop delay near 2500–3000 viewers once the path is wider. Fix idea, out of scope: stringify once per change, coalesce moves per tick.
  - scripts/stress/ on main; throwaway deleted; live health exposes `load` read-only.
- kr_giqd28iwcb (off-site backup): not started; proposal gr_jkorz4f49a filed, waiting on you.
- kr_wm6mphmrjf (token rotation): not started; no proposal (one open proposal per building). Next in line once the backup grant is decided.

## Needs from Mitchell
1. **Close out the stress grant:** mark kr_z9lcfnvt94 met (or cut gr_wqnunw5yd8) from the evidence above, since the 100% checkpoint can't be filed by me below the trigger. Funding or countering gr_jkorz4f49a is a separate in-tray item.
2. **FLY_STRESS_TOKEN is an org-wide Fly token and the throwaway is gone:** revoke it, or re-scope it to an app-scoped deploy token if you want future throwaway runs.

