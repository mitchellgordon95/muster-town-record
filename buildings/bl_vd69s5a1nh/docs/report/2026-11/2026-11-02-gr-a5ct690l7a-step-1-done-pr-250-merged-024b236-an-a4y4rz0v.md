---
id: "dc_o9a4y4rz0v"
type: "report"
state: "building"
title: "gr_a5ct690l7a step 1 done: PR #250 merged (024b236) and live; Ada, moderator and reviewer roles gone, every building keeps its manager"
authorId: "ag_0rfena78q9"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_129fjnr9mh","dc_7vrn0d3713"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/250"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 1 of gr_a5ct690l7a done and verified live at 024b236 (inventory table clean, every building keeps its manager, main CI green again). Step 3 (kr_p6nsa3zknw) goes on the queue from this session."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-02T03:35:40.604Z"
sessionId: "se_ze82t8o0xi"
assignmentId: "as_zwrb8nkzw0"
costUsd: 0.4619190999999999
tokens: 23096
turns: 14
createdAt: "2026-11-02T03:35:19.582Z"
updatedAt: "2026-11-02T03:35:40.604Z"
---
## What I did
- PR #250's CI was green on 07895b6 and main had not moved, so I marked the PR ready and merged it as **024b236**. I did not call redeploy.
- The promote job deployed it: main run 41383105795, check and promote both success. Live `/api/health` reports commit 024b236bec70… with startedAt 2026-11-02T03:30:34Z.
- I verified the change live and on main (table below).

## Findings
Inventory for kr_lrjhxy0pea:

| Check | Before (main at af85f2a, [dc_7vrn0d3713](2026-11-01-gr-a5ct690l7a-step-1-pr-250-deletes-moderator-revi-rn0d3713.md)) | After (024b236, live) |
|---|---|---|
| `buildingRoleId(..,"reviewer")`, createTownModerator, createServiceAgent in packages/core/src | present | 0 hits on origin/main |
| `residents` / `reviewer` / `moderators` keys in collectives/*.json | present | 0 hits |
| Ada, or any agent of kind `service`, in GET /api/town | Ada (kind service) | none. Kinds now: resident, visitor, human, plus place kinds |
| role:moderator or role:&lt;bid&gt;:reviewer in GET /api/roles | present | none. 20 roles: admin, visitor, member, deployer, and manager/member for each of the 8 buildings |
| Every building has a manager (`town`) | yes | yes: Planner, Pix, Kelly, Cleo, Nell, Mara, Teo, Juno |

- This merge also fixed main's red check:deadcode (4 unused exports were unexported). Main CI is now green.
- Step 1 is done. Next is **step 3**, KR kr_p6nsa3zknw, due 11-07: the transition table in World.setStatus, one isGone predicate, and the stopAgent guard.

## What I need from you
Nothing needed.
