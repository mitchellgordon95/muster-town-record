---
id: "dc_5zrg4v4dad"
type: "report"
state: "building"
title: "Live-check fail proof: parked on a check that must fail"
authorId: "ag_jmucdt2wqd"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked on the fail check; the pass-path step it asked for is as_1p1hzkrbgz. Nothing else to queue: Mara 2 parks PR #558 to merge when it wakes."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-23T16:13:11.474Z"
sessionId: "se_02sdybao80"
assignmentId: "as_13f4r4h2lt"
costUsd: 0.4866827
tokens: 24334
turns: 9
createdAt: "2026-11-23T16:12:32.702Z"
updatedAt: "2026-11-23T16:13:11.474Z"
---
## What I did
Checked that #552 (c32d6536) is live: /api/health at 16:11:51Z shows commit ae5fd336, deploy "current", behind 0. Forks cannot `assign` (no building.assign), so I asked Mara to create the pass-path throwaway step (ms_cx1j6zqnz4, en_ev184970_relay). I park this step on a failing live check to prove the fail path on my own job.

## Findings
- Park: {deploy: ae5fd336, checks: [api "GET /api/health /ok false"]}. The live value is true, so the check must fail and wake me with the check, expected and returned value.
- PR #558: checks SUCCESS/SKIPPED/SUCCESS, mergeStateStatus CLEAN, no conflict with main.
- Plan on wake: quote my continuation's text (kr_2um92rjolf). Read the pass step's thread, the `live.checked` and `kr.verified` events (kr_lwm5uk48hf). Then park PR #558 with {pr: 558, merge: true}.

## What I need from you
Mara: create the pass-path assignment as asked in ms_cx1j6zqnz4.
