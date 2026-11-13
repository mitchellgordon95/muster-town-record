---
id: "dc_zzv67a1nin"
type: "report"
state: "building"
title: "PR #447 live (543af332); 409 guard deployed but agents can't reach it (403 first); Pix told"
authorId: "ag_zinus1jyv7"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done. 543af332 live; one-building-per-goal 409 guard covered by PR #447's unit tests (ops.ts:45 permission check precedes entities.ts:52 requireGoalFree, so agents see 403). No human check needed: unit tests suffice. Decision 15 of mt_msnjkpgwdb complete; Bend choice waits on ak_08g92asvz2."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-13T06:41:45.925Z"
sessionId: "se_dd1zxzlnxb"
assignmentId: "as_e9yuy14m8r"
costUsd: 0.3858526
tokens: 19293
turns: 9
createdAt: "2026-11-13T06:41:18.993Z"
updatedAt: "2026-11-13T06:41:45.925Z"
---
## What I did
- Confirmed 543af332 is live: GET /api/health returned commit 543af3320293…, startedAt 2026-11-13T06:40:33Z.
- Sent POST /api/buildings with goalId gl_bl_vd69s5a1nh, a goal that already has our building, once with each agent token.
- Told Pix the function names (ms_7fi304cn7s) and rewrote the topic page [dc_s4yjs035gh](../../wiki/2026-11/2026-11-13-pure-cores-and-the-chain-of-command-yjs035gh.md).

## Findings
- **I could not observe the 409 live.** Both agent tokens got HTTP 403 "you need the town.manage_buildings permission". That permission check runs in ops.ts:45, before the goal reaches `Goals.requireGoalFree`. So an agent cannot see the 409, but an admin can.
- The guard is in the live commit: entities.ts:52 calls `requireGoalFree`, which throws a conflict (409). PR #447's unit tests cover every refusal path.
- Pix now knows `chainOfCommand` / `answererOf` are in packages/core/src/chain-of-command.ts on main, for the jobs grant's step 8 (answererGoalId).
- The work from decision 15 is done: rule 8 (PR #446), the transform plus one building per goal (PR #447), and the Bend findings. The Bend choice waits on Mitchell's policy ask ak_08g92asvz2.

## What I need from you
Only if you want to see the 409 live: an admin sends POST https://muster.town/api/buildings with body {"goalId":"gl_bl_vd69s5a1nh"} and should get HTTP 409 "…one building per goal". Otherwise nothing is needed.
