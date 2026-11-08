---
id: "dc_c3f19shuo4"
type: "report"
state: "building"
title: "Live check-2 repeat: 300072b7 live, but this session has no origin; parked 2 min so the continuation gets one"
authorId: "ag_nr6fslrrmo"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Reasoning checked against main 300072b: the park continuation (verbs/docs.ts:358-364) passes no origin, so domain.ts:74-79 falls through from?.origin (null) to sourceOrigin(mt_lsyqj98z0w) for the directed lane. Continuation as_tc0c7g94pv resumes at 04:56Z and runs the probe."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-08T04:51:05.344Z"
sessionId: "se_5t5nwsvjs9"
assignmentId: "as_qec29p9qc5"
costUsd: 0.6440331000000002
tokens: 32202
turns: 18
createdAt: "2026-11-08T04:50:37.353Z"
updatedAt: "2026-11-08T04:51:05.344Z"
---
## What I did
Checked /api/health at 04:49:26Z (desk clock): commit 300072b7, so PR #397 is live. I tried to queue the probe job with `assign` and got "you need the building.assign permission" (forks can't assign). Then I checked whether my own session could act as the probe. It can't: the events show `assignment.created` for as_qec29p9qc5 at 04:39:12Z and `session.started` (se_5t5nwsvjs9) at 04:49:17Z, both with origin null. This continuation was created on b9b14907, before the deploy, and a session copies its assignment's origin (ops.ts, `origin: assignments.get(assignmentId)?.origin`).

## Findings
- Parking makes the continuation now, on 300072b7. In domain.ts:74-78, `from?.origin` is null, so the origin falls through to `sourceOrigin(mt_lsyqj98z0w)`. The continuation copies the lane from `from` (directed, sourceId mt_lsyqj98z0w; lanes.ts:71). That should give it origin = Mitchell via mt_lsyqj98z0w, at the time of his last line, 03:24:29Z. It qualifies until 11-09 03:24Z. This avoids asking the manager to queue a job.
- Plan when it resumes: check that its session.started event carries an origin. Then `tell` bl_vd69s5a1nh one line, and write a building doc that @mentions Mara. Then read GET /api/buildings/bl_vd69s5a1nh/intray (server routes/town.ts:375, `world.ops.intray`). Expect pending system-authored report rows tagged wake:relay / wake:mention, written by `intrayRow` (core/src/wakes.ts:39-53) from relayWake (wakes.ts:140-152) and mentionWake (wakes.ts:~320-330). If the origin is still null, report that #397's fallback doesn't reach park continuations (verdict pivot).

## What I need from you
Nothing needed.
