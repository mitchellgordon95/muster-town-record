---
id: "dc_imjka87kxt"
type: "report"
state: "building"
title: "Map shape mocks: three layouts of the live tree (note dc_fvgi5nq36j); recommend (a) fountain plazas"
authorId: "ag_qecf6mofro"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_wql34b8gkl","dc_fvgi5nq36j","dc_4su2e5yyhn","dc_hai9ky5u7a"],"urls":["https://muster.town/api/goals"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: three mock layouts (a fountain plazas mf_acetqtaoqe, b plain tree mf_7203o6ba8x, c radial mf_shxe83fsdq) in note dc_fvgi5nq36j, recommendation (a). Mitchell's pick goes in rollup 35 Needs item 2 (already on dc_hai9ky5u7a). Building the picked shape is queued only after he picks (directed, mt_wql34b8gkl)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T18:24:07.535Z"
sessionId: "se_ni9lf3p5dn"
assignmentId: "as_jrcext47n2"
costUsd: 0.9257200999999999
tokens: 46286
turns: 21
createdAt: "2026-10-31T18:23:53.830Z"
updatedAt: "2026-10-31T18:24:07.535Z"
---
## What I did
Read the live tree from `GET /api/goals`. Applied the PR #168 folding rules and drew three layouts with a throwaway PIL script on my desk (`~/mock/draw.py`), all at the same scale (lot 84×40 px, road 10 px, 300 px tall), with the real goal names on signposts. Uploaded the pictures and filed the note **[dc_fvgi5nq36j](../../note/2026-10/2026-10-31-map-shape-mocks-three-layouts-of-the-live-tree-gi5nq36j.md)**, "Map shape mocks: three layouts of the live tree". Updated the topic pages [dc_hai9ky5u7a](../../wiki/2026-10/2026-10-31-rollup-35-materials-i9ky5u7a.md) (Needs item 2: pick a layout, with the ids) and [dc_4su2e5yyhn](../../wiki/2026-10/2026-10-31-how-work-gets-done-vision-doc-u2e5yyhn.md) (build-order state). No production code changed, so no PR.

## Findings
- Live tree on 2026-10-31 ~19:20Z: **20 goals, 7 buildings**. After folding, the map draws 2 first-level goals (Steer with the Workshop; Trust with no building of its own), 5 lower goals with one building each, the Town Hall and the Bank. Fund has no buildings, so it is not drawn.
- (a) Fountain plazas at level 1, streets below: ![a](/api/media/mf_acetqtaoqe.png) **mf_acetqtaoqe**. It reads most like a town and related buildings share a plaza. Today each street holds only one lot, so the plazas look oversized. At 3× (~20 buildings) the streets fill up and the layout stays stable.
- (b) Plain tree: ![b](/api/media/mf_7203o6ba8x.png) **mf_7203o6ba8x**. It is the clearest and most compact today (640 px) but looks like an org chart. At 3× it becomes a strip ~1900 px wide.
- (c) Radial: ![c](/api/media/mf_shxe83fsdq.png) **mf_shxe83fsdq**. It has a clear centre but diagonal roads and empty corners. At 3× it needs ~600 px of height, and every new sibling moves all the spokes, which breaks the stable-layout rule.
- **Recommendation:** (a). It is the only shape that gets better as the tree grows. While a lower goal has only one building, that building can sit on the plaza's rim.
- Building the picked shape is not queued yet. Queue it (directed, mt_wql34b8gkl) once Mitchell picks.

## What I need from you
Mitchell: pick a map layout (a, b or c) from [dc_fvgi5nq36j](../../note/2026-10/2026-10-31-map-shape-mocks-three-layouts-of-the-live-tree-gi5nq36j.md). It is already listed under Needs in rollup 35.
