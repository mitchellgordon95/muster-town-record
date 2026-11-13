---
id: "dc_j01zx1o0qn"
type: "report"
state: "building"
title: "Chain of command as a pure function + one building per goal: PR #447 open, waiting on CI"
authorId: "ag_3bk3ltdc2z"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked report; the continuation (as_rufjlw20cl, waits on PR #447 CI) merges and parks on deploy. Nothing else to queue."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-13T06:21:29.873Z"
sessionId: "se_5gw4ql0vqx"
assignmentId: "as_fts38a0zxd"
costUsd: 2.5615145999999998
tokens: 128076
turns: 49
createdAt: "2026-11-13T06:21:10.510Z"
updatedAt: "2026-11-13T06:21:29.873Z"
---
## What I did
Wrote the pure chain-of-command transform with property tests and the narrowed one-building-per-goal rule, both in one PR: https://github.com/mitchellgordon95/muster-town/pull/447 (draft). `npm run check --fast` passed on the desk, and so did the targeted core, server and runtime tests (about 40 files, run in batches). Parking until CI finishes, then I merge.

## Findings
- **Function name for Pix (step 8):** `chainOfCommand` in packages/core/src/chain-of-command.ts. You pass in goals {id, parentId, ownerId}, buildings {id, goalId} and rootId. You get back a Map from buildingId to {answererGoalId, userId|null}. For a single goal, use `answererOf(goalId, lookup, rootId)`. `Goals.ownerOf`, `route` and `tree()` now call it, so the rule lives in one place.
- **Property tests (fast-check, added as a core devDependency):** every building gets exactly one answerer. The answerer is an ancestor of the building's goal, or the goal itself. It is captained unless it is the root, and it is the nearest such goal. Adding a captain never moves an answerer upward. Two more tests: Mitchell's UI / UX example (it answers to the root, past the Workshop), and a check that the live `route` agrees with the function.
- **One building per goal:** `Goals.requireGoalFree` makes createBuilding (and through it POST /api/buildings, adopt and import), attach, and retire's moveTo refuse a goal that already has a lab on it, with 409. Nesting is still allowed. The root is exempt because it is where a building with no goal picked lands (seeds, imports, tests). The Town Hall is exempt too. A goal move never changes which goal a building is on, so it is not checked. Import always builds at the root, so it has nothing to refuse.
- **Shared lookup and adopt:** `Goals.nearestBuilding` replaces entities.ts `labOnChain` and the unused `Goals.buildingNear`. I kept adopt's refusal when a lab is above the goal: it is the visitor path (register there instead), and the existing visitor-managers tests depend on it.
- **Tests and docs:** 3 old tests that put two labs on one goal were moved onto sibling or child goals. The design line (pure core plus property tests) is now AGENTS.md standing rule 8. docs/goals.md has new "Chain of command" and "One building per goal" sections. Log entry: docs/log.d/2026-11-13-mara-2-chain-of-command.md.
- **Live tree:** no goal on the live tree has two buildings today (read 2026-11-13), so nothing on muster.town breaks.
- **Not started from decision 15:** the Bend 2 investigation, and reviewing the jobs-grant PRs for the pure-core shape. Topic page: [dc_s4yjs035gh](../../wiki/2026-11/2026-11-13-pure-cores-and-the-chain-of-command-yjs035gh.md).

## What I need from you
Nothing needed. After CI I merge PR #447. Once it is deployed, the check is that POST /api/buildings on a goal that already has a building returns 409.
