---
id: "dc_wy7maaho1k"
type: "report"
state: "building"
title: "Grant gr_a5ct690l7a adjusted: 1,000,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:99558:bl_vd69s5a1nh"]
decision: "approve"
decisionNote: "Acknowledged: Mitchell lifted gr_a5ct690l7a from 350,000 to 1,000,000 tokens at its checkpoint (371,124 spent, 628,876 left), enough for all four steps by the checkpoint's estimate. The held continuation as_f1hpgeoxn4 assumed PR #250's CI had finished on green, which never happened (the PR conflicts with main, GitHub ran no CI), so I cancelled it and queued an accurate step-1 finish on the building queue (merge main, resolve, CI, merge, verify live). Steps 3, 2, 4 follow one at a time from each step's report."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-02T03:00:59.642Z"
createdAt: "2026-11-02T02:59:46.800Z"
updatedAt: "2026-11-02T03:00:59.642Z"
---
Written by the town: Mitchell adjusted grant gr_a5ct690l7a at its checkpoint (event 99558, 2026-11-02 02:59 UTC).

## Summary

Grant gr_a5ct690l7a "One agent model (managers with forks, visitors, humans), with agent status as one core state machine and visitors adding capacity to goals: leftover multi-resident code gone first." adjusted by Mitchell: 1,000,000 tokens.

Status funded; 371,124 of 1,000,000 tokens spent; key results kr_lrjhxy0pea [at-risk] One agent model: the town moderator role, the building reviewer role, the per-building residents list in collective.json and Ada (kind service) are gone from core, seed, the spec and the web mock; a fresh seed creates only the planner and each building's manager.; kr_ie3i3swby4 [not-started] A visitor picks a goal with desks and gets a desk beyond headcount while they work there (released on leave/offline); the manager's fork count is unchanged and the visitor's tokens show on the goal as contributed, drawn from no Bank balance and outside the goal's cap.; kr_p6nsa3zknw [not-started] Agent status is one transition table in World.setStatus and one predicate answers 'is this agent gone?': stop, resume, a meeting invite or a review continue on a dismissed or banned agent is refused (409) and its status stays; inline checks drop from 122 to under 10, SKIP_STATUSES gone.; kr_8a7vskwse2 [not-started] A visitor adopting a goal with no desks becomes its building's manager: the building is created on the goal if missing, manager channels (in-tray, flags, 1:1s, tells, rollups) reach the visitor, assign-to-queue is refused for them, and on leave the building holds its queue..

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
