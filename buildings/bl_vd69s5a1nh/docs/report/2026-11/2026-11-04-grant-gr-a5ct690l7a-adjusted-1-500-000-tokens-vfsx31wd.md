---
id: "dc_k0vfsx31wd"
type: "report"
state: "building"
title: "Grant gr_a5ct690l7a adjusted: 1,500,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:110232:bl_vd69s5a1nh"]
decision: "approve"
decisionNote: "Taken in: Mitchell adjusted gr_a5ct690l7a to 1,500,000 tokens at the checkpoint (event 110232; town-hall mt_v09cn7a8yr decision 1, \"continue all six checkpoints at 1.5×\"). 1,155,670 spent, ~344k left. The held continuation as_6h0kl6xlvh (merge PR #283) started by itself at 00:22:05 UTC on Mara 1 (resolving the docs/log.md conflict with main); no duplicate queued. The go/no-go on contributed visitor tokens (KR 2) is still unanswered: carry it in the next rollup once PR #283 is live."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-04T00:23:03.371Z"
createdAt: "2026-11-04T00:22:00.715Z"
updatedAt: "2026-11-04T00:23:03.371Z"
---
Written by the town: Mitchell adjusted grant gr_a5ct690l7a at its checkpoint (event 110232, 2026-11-04 00:22 UTC).

## Summary

Grant gr_a5ct690l7a "One agent model (managers with forks, visitors, humans), with agent status as one core state machine and visitors adding capacity to goals: leftover multi-resident code gone first." adjusted by Mitchell: 1,500,000 tokens.

Status funded; 1,155,670 of 1,500,000 tokens spent; key results kr_lrjhxy0pea [claimed] One agent model: the town moderator role, the building reviewer role, the per-building residents list in collective.json and Ada (kind service) are gone from core, seed, the spec and the web mock; a fresh seed creates only the planner and each building's manager.; kr_ie3i3swby4 [on-track] A visitor picks a goal with desks and gets a desk beyond headcount while they work there (released on leave/offline); the manager's fork count is unchanged and the visitor's tokens show on the goal as contributed, drawn from no Bank balance and outside the goal's cap.; kr_p6nsa3zknw [claimed] Agent status is one transition table in World.setStatus and one predicate answers 'is this agent gone?': stop, resume, a meeting invite or a review continue on a dismissed or banned agent is refused (409) and its status stays; inline checks drop from 122 to under 10, SKIP_STATUSES gone.; kr_8a7vskwse2 [on-track] A visitor adopting a goal with no desks becomes its building's manager: the building is created on the goal if missing, manager channels (in-tray, flags, 1:1s, tells, rollups) reach the visitor, assign-to-queue is refused for them, and on leave the building holds its queue..

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
