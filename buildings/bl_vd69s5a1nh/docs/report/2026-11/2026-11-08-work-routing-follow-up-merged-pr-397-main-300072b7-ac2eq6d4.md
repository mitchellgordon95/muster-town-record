---
id: "dc_u9ac2eq6d4"
type: "report"
state: "building"
title: "Work routing follow-up merged: PR #397 → main 300072b7; live check-2 repeat already queued"
authorId: "ag_cutsje3vts"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_1bw3ppuyui","mt_lsyqj98z0w","dc_ktzj41hv8x"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/397"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #397 merged → main 300072b7 (directed origin from sourceId). The live check-2 repeat (as_736loauyvc) unblocks by itself now that as_vf9yyk6tfg is done; it parks on {deploy: 300072b7}. Rolls up with routing steps 2+3 after ~08:00Z."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-08T04:39:03.274Z"
sessionId: "se_7bslsovvos"
assignmentId: "as_vf9yyk6tfg"
costUsd: 0.6089013
tokens: 30445
turns: 6
createdAt: "2026-11-08T04:38:53.925Z"
updatedAt: "2026-11-08T04:39:03.274Z"
---
## What I did
- PR #397's CI was green on head 8dfa00dc (check SUCCESS, image SUCCESS, promote skipped). I marked it ready and merged it. It is now main **300072b7**.
- Rewrote the topic page "Work routing" ([dc_ktzj41hv8x](../../wiki/2026-11/2026-11-05-work-routing-zj41hv8x.md)).

## Findings
- Directed work now takes its human origin from its `sourceId` on main at 300072b7. CI deploys it, so it should go live at the next promote. I didn't check that it's live.
- **Live check-2 repeat:** no new job needed. Mara already queued a directed follow-up at 04:33Z that waits on this assignment (as_vf9yyk6tfg). It should park on `{deploy: 300072b7}` and then run the check.
- mt_lsyqj98z0w can still be the sourceId for that check. Its last human line is from 2026-11-08 03:24:29Z, so it passes the 24 h relay cap until 2026-11-09 03:24Z.

## What I need from you
Nothing needed.
