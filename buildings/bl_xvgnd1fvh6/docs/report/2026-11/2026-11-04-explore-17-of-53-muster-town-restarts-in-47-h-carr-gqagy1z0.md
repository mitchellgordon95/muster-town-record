---
id: "dc_6xgqagy1z0"
type: "report"
state: "building"
title: "Explore: 17 of 53 muster.town restarts in 47 h carried no new code; proposed gr_lvzy0yxwgd (90k) to stop no-op redeploys"
authorId: "ag_cp37l46nqb"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_abyhrunhjo","dc_vzqoh7ppen"],"urls":["https://muster.town/api/events?since=104000","https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Checked the claim against main at edb3201: redeploy.ts:260–301 pulls, counts the commits (since()), then rebuilds and drains regardless of whether the count is 0. Finding stands. gr_lvzy0yxwgd is in the Town Hall in-tray on its own; nothing more to assign until Mitchell decides it."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T18:02:08.441Z"
sessionId: "se_spbm3qaj3b"
assignmentId: "as_fmbavxn9e3"
costUsd: 1.1153673000000002
tokens: 55768
turns: 25
createdAt: "2026-11-04T18:01:47.631Z"
updatedAt: "2026-11-04T18:02:08.441Z"
---
## What I did
- **Ruled out the other gaps under the hosting goal first.** Token rotation was dropped by Mitchell. Disk, backups and outside alerting are already covered (monitor.ts and the VPS pinger).
- **Measured restarts from the live event log**, covering 2026-11-02 18:21Z to 2026-11-04 18:00Z.
- **Wrote up the findings** as [dc_abyhrunhjo](../../note/2026-11/2026-11-04-findings-one-in-three-muster-town-restarts-brings-yhrunhjo.md).
- **Proposed gr_lvzy0yxwgd** (90,000 tokens).

## Findings
- **53 restarts in about 47 h.** Health `capacity.restarts24h` reads 24 right now. Each restart is down for only 2.9–4.4 s (median 3.3 s).
- **17 of the 53 (32 %) restarted with "0 new changes".** All 17 were agents calling `redeploy` straight after a merge, before CI had moved `prod`: Nell 1 ×5, Teo 1 ×5, Pix 1 ×4, plus Pix 3, Mara and Teo 2.
  - 13 were followed within 1–18 min by the restart that did carry the changes. Six of those were CI's, exactly 15 min later, because CI waits until the server has been up 15 min.
  - So each no-op restart delays the real deploy by up to 15 min.
  - It also adds a drain: 886 s in total, during which new work is held and team-lead sessions are interrupted.
- **Cause.** `packages/runtime/src/redeploy.ts` always restarts. And both the tool's description and the town-wide merge-rules FYI ([dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-10-30-schema-mi-qoh7ppen.md)) still tell agents to call `redeploy` after a merge.
- **Proposal gr_lvzy0yxwgd.** When there is nothing new on prod compared with the running commit, the redeploy ends without restarting. A deliberate restart (with a reason) or an image deploy still restarts. The proposal also rewrites the tool text and the merge-rules FYI, then counts restarts live for 3 days.
- **Overlap with gr_w9ue1k1p0c.** That grant makes cut sessions end as interrupted and resume; this one removes about a third of the cuts at their source.

## What I need from you
Decide whether to fund gr_lvzy0yxwgd.
