---
id: "dc_oyvkqa06g6"
type: "report"
state: "building"
title: "Goal tree step 2 merged (PR #123, 0122bf1): the map is drawn from the goal tree; live check parked"
authorId: "ag_l304ok8p2r"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #123 merged as 0122bf1, checks green, no migration, no Bank change. Live check already parked as as_9u565tt6k8 (waiting on deploy 0122bf1); its report will carry the screenshot for rollup 33. Your two calls (empty goal = empty 4-tile plaza with signpost; long walks left as-is) go to Mitchell as the Your call line."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T22:15:53.268Z"
sessionId: "se_1dwszi46fo"
assignmentId: "as_8thp76uzbm"
costUsd: 0.9267305999999998
tokens: 46337
turns: 28
createdAt: "2026-10-30T22:15:39.588Z"
updatedAt: "2026-10-30T22:15:53.268Z"
---
## What I did
- Recovered the previous session's work (as_jk5v8pbw7a) from desk stash@{0}: 36 files. Committed and pushed it as 0e6f9ae by turn 5.
- Ran `npm run check`: all green. Fed the live tree (GET /api/goals, /api/town) through the new layout and drew it as text to check it.
- Opened and merged https://github.com/mitchellgordon95/muster-town/pull/123. Merge commit: **0122bf1**. Queued the redeploy.

## Findings
- **What changes:**
  - `core/world/tree.ts` `treeLayout` computes every building's position (its lot) and every plaza from the goal tree.
  - The Town Hall stands at the root above the root plaza, with the Bank below it (`BANK_LOT` now at y 14).
  - Each goal gets a plaza with a signpost: place `plaza:<goalId>`, named with the goal's text. The root keeps the old place id `plaza`. Objectives (ob_*) are goals, so they get plazas too.
  - Each lab hangs below its goal's plaza, with its door in the top wall.
  - Child goals sit below their parent in a fixed order. Each goal's column band is rounded up to 8 tiles, so adding a child moves nothing to its left.
  - Roads are the plazas plus the tree's edges, drawn like an org chart. The two trunk road rows are gone.
- **What goes:**
  - `plan.ts`, `PUT /api/town/plan`, and dragging to move, resize or draw buildings.
  - The town map is now a read-only overview for everyone. Clicking a building shows "Attached to: <goal path> · Change…".
- **How buildings are sized and placed:**
  - The Desks setting (headcount) sets a building's size.
  - The planning desk's create form Goal picker places a new building.
  - Any goal event (created, edited, moved, retired, attached) redraws the map, and bodies move with it (`followRelayout`), including across a deploy.
- There is no migration and no Bank accounting change.
- **The two open questions (my calls; Mitchell may overrule):**
  1. An empty goal (no building, no key results) is drawn as an empty 4-tile plaza with its signpost, so the gap shows.
  2. Long walks on deep trees: left as they are for now. Levels are 3 rows apart and roads run straight; nothing is folded.
- **The live tree, drawn from the new code:**
  - About 175×50 tiles: the root band, then 9 child bands.
  - Fund, Join and Trust show as empty plazas.
  - Workshop has 3 objective plazas below it, Prod has 2, Code Legibility has 1.
  - Every door opens onto its plaza.
- **Tests:** `npm run check` green: typecheck, docs and deadcode checks pass. Core 498/498, server 157/157, web 149/149, other packages all pass. New test file: `core/test/tree.test.ts`.
- **Not yet verified:** the live deploy and a screenshot. When the work resumes it will check that `/api/health` reports commit 0122bf1 and that the live map shows the plazas and roads, then take the mf_ screenshot. Topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md) is updated.

## What I need from you
Nothing needed.
