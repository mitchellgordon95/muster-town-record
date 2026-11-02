---
id: "dc_9fvas4elzt"
type: "report"
state: "building"
title: "gr_a5ct690l7a funded: step 1 (delete moderator, reviewer, residents list and Ada; fresh seed = planner + managers) queued as as_7y9xdesm82; steps 2–4 follow one at a time"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_87vz2ppews","dc_04z45ot157","dc_3yqhz2qidx"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 1 of gr_a5ct690l7a is queued as as_7y9xdesm82 and Mara 2 is running it; steps 2–4 queue from each step's report. Nothing further to assign."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-01T02:05:48.406Z"
sessionId: "se_2j0ecfqy8t"
assignmentId: "as_9654757otm"
costUsd: 1.2280784
tokens: 61404
turns: 10
createdAt: "2026-11-01T02:05:27.914Z"
updatedAt: "2026-11-01T02:05:48.406Z"
---
## What I did
Read the funded plan and the topic page [dc_87vz2ppews](../../wiki/2026-11/2026-11-01-agent-lifecycle-status-state-machine-vz2ppews.md), re-took the deletion inventory on the code snapshot (main af85f2a), and queued the first step to the building queue in lane grant (gr_a5ct690l7a) with the three topic pages that cover it. Rewrote [dc_87vz2ppews](../../wiki/2026-11/2026-11-01-agent-lifecycle-status-state-machine-vz2ppews.md) with the step list and the inventory numbers; logged it.

## Findings
The plan already splits into four PRs, each one session's worth with a live check, so the steps are the PRs, one assignment each, queued in order from the previous step's report (each must be merged and live before the next starts, so I don't chain them with waitFor: a parked PR continuation would fire the next step too early).

- **Step 1, QUEUED: as_7y9xdesm82** (KR kr_lrjhxy0pea, due 2026-11-07). Inventory first, then delete. Counts on af85f2a that the fork records as "before": buildingRoleId reviewer 4 call sites in packages/core/src; "reviewer" 29 lines in 7 core files; "moderator" 34 lines across core, runtime and server src; createTownModerator in core index.ts, entities.ts, seed.ts and 3 tests; createServiceAgent in 3 files; kind "service" 4 lines (plus 6 in web); web mock Wren/Ada 8 lines; collectives/workshop/collective.json still has "moderators", "residents" and "reviewer" keys, read by seed.ts:234/240. Also includes migrate-roles dropping the dead roles, a fresh-seed test (planner + one manager per building), doc updates for check:docs, and the stop-early rule if a live building depends on a reviewer or residents list. Human check when live: the grep in the KR finds nothing on main and the collective.json has none of the three keys.
- **Step 2** (kr_ie3i3swby4): registerVisitor takes goalId, desk beyond headcount (grow), excluded from freeDesks, released on offline/leave, contributed tokens on the goal page, never Bank-metered. Stops and asks Mitchell if keeping it out of the Bank cap needs Bank code.
- **Step 3** (kr_p6nsa3zknw): TRANSITIONS table in World.setStatus, one isGone predicate (122 inline checks → under 10), docs/invariants/agent-lifecycle.md linked from AGENTS.md; the dismiss → stop → resume revival bug closes here.
- **Step 4** (kr_8a7vskwse2, due 11-10): adopt verb for a visitor on a goal with no desks. The grant's stop condition lets this become a follow-up grant if steps 1–3 use the tokens.

Nothing else is on the queue. Next wake for me: step 1's report (continue → step 2) or its park on CI/deploy.

## What I need from you
Nothing needed.
