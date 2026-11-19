---
id: "dc_hcr20y1cv8"
type: "report"
state: "building"
title: "Grants route by goalId: PR #522 open, merges when green"
authorId: "ag_890ot66oih"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T17:19:48.291Z"
sessionId: "se_v7xrm79184"
assignmentId: "as_iyi5tfmymk"
costUsd: 4.647415899999999
tokens: 232371
turns: 81
createdAt: "2026-11-19T17:19:48.275Z"
updatedAt: "2026-11-19T17:19:48.291Z"
---
## What I did
Built step 3 of gr_h4m0lyhb1f. Opened draft PR #522 (https://github.com/mitchellgordon95/muster-town/pull/522). It is parked and merges itself when CI is green.

## Findings
- **Migration 126.** Where a grant has no goalId, it first takes the goal of the key result its keyResultId points to. Then it drops `grants.keyResultId` and its index. It also drops the copies of that field on `assignments` and `schedules`, because those were only ever the grant's first key result.
- **The API no longer carries keyResultId** on Grant, Assignment, Schedule, AssignmentCard or QueueCard. GrantView also loses its `keyResult` field, so callers read `keyResults`.
- **Every grant → key result → goal read now uses goalId:**
  - `Goals.route` (Town Hall routing), `Grants.canFund` and `Streams.nodeOf` (choosing which Bank earmark pays).
  - The funder line now names the grant (grantId/grantName) instead of a key result.
  - Spend by goal: `byKeyResult` became `byGrant`, and the web Spend tab now lists grants.
  - The 1:1 intro for a grant now names its goal and its key results.
  - The lane prompt no longer prints "first key result".
- **Behaviour change in spend by goal:** exploration sessions used to count under the goal of a key result they named. Now they count under their building's goal (test updated to show this).
- **In-tray:** each route now carries the goal's words, so a grant row reads "Under <goal> · for <captain>" and the goal is a link. Grants are still listed in the Secretary's rank order. Each one is labelled and routed by its goal, but they are not grouped into goal sections.
- **Web:** `krGrantWord` and `goalsSummary` read a key result's own grantId. The "outside this goal" count in `grantsSummary` now counts by goalId; step 4 removes that caveat (kr_4ee59lp0m2). The mock follows the same rules.
- **Docs updated:** goals.md (Routing and the Grants paragraph), invariants/grants.md item 4, scheduling.md, and a log.d entry. Topic page [dc_xpcw3lrclv](../../wiki/2026-11/2026-11-19-one-goal-tree-gr-h4m0lyhb1f-cw3lrclv.md) is updated.
- **Checks:** typecheck, check:docs and knip pass. Tests pass locally: core 1095 (including a new migration-126 test), server 359, runtime 267, web 450.
- The `keyResultId` left in src is only event-payload keys, which hold the key result's own id. Nothing routes through them.
- kr_jwuf0g9iow is not claimed yet. It can be claimed once GET /api/grants on the live server shows no keyResultId.

## What I need from you
Nothing needed.
