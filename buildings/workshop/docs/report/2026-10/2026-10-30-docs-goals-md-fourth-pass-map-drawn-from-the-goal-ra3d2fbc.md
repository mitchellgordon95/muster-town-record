---
id: "dc_kira3d2fbc"
type: "report"
state: "building"
title: "docs/goals.md fourth pass: map drawn from the goal tree, 1:1 mt_kh0zaqui0w answers, UI inventory; PR #116 head 0656bd7 (not merged)"
authorId: "ag_ehlkvsd0aa"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #116 at 0656bd7 (map from the tree, Q1-Q4 folded in, UI inventory). Q5-Q7 answered in mt_kh0zaqui0w (owners fund, humans only; prep reports or 24 h; skip-level dropped); a fifth pass folds them in with the key-rule answer once Mitchell gives it."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T20:30:19.593Z"
sessionId: "se_6k6ml4493h"
assignmentId: "as_hjwljl7eb8"
costUsd: 1.4826968999999999
tokens: 74135
turns: 27
createdAt: "2026-10-30T20:30:12.250Z"
updatedAt: "2026-10-30T20:30:19.593Z"
---
## What I did
Rewrote docs/goals.md on the PR #116 branch for 1:1 mt_kh0zaqui0w. This is docs only. I committed it as **0656bd7**, pushed it to agent/pix-2/design-doc-docs-goals-md-town-level-goal and confirmed origin has it. Not merged. PR: https://github.com/mitchellgordon95/muster-town/pull/116. Topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md) is rewritten.

## Findings
- **New section "The map is the tree".** The Town Hall sits at the root. Each goal is a plaza (`plaza:<goalId>`) with a signpost. The roads are the tree's edges, so the trunk rows go. Each building stands at the goal it is attached to, so walking from the Town Hall to a building walks down the tree.
  - Drag placement, drag-resize and drawing new buildings on the planning side bar all go. The code from PR #83 (`computeLayout`, `deriveRoads`, `validatePlan`) becomes the renderer for a new `treeLayout`.
  - Consequences written in: building size now comes from the Desks setting, the create form gets a Goal picker, any tree change redraws the map and bodies re-path, and the map's size limits become derived.
  - Exactly one attachment per building. The layout is stable and seeded: children keep a fixed order and each band keeps room for one more child, so adding a sibling moves no earlier building.
  - Left open for Mitchell: what an empty goal looks like, and long walks on deep trees.
  - In the build order it is **step 2**, right after the core. The old steps move down one, and "new dials" is dropped.
- **Answers folded in:**
  - **Q1:** KPIs are parked. No dials in the tree, no dial slides and no dial-target KRs.
  - **Q2:** retiring a goal offers move-to-sibling and is refused when no sibling is picked. Attached buildings get the same rule.
  - **Q3:** one root with Fund/Join/Trust as placeholder children, depth unbounded, KRs always dated leaves.
  - **Q4:** `buildings.goalId` replaces the `building_goals` table. It is required at creation (default: the root), editable in settings, and never unset.
- **Migration changed to fit one attachment per building.** Every building gets its own goal `gl_<buildingId>` under the root and is attached there. Its objectives (same ids) sit under that goal. Fund/Join/Trust start empty. Result: 16 goals, 31 KRs (19 open, 12 archived), and two buildings blocked: Bank Transparency and UI / UX. Moving goals under Fund/Join/Trust is left to Mitchell. The migration section links the KR inventory **[dc_io1ry1ryjz](../../note/2026-10/2026-10-30-every-key-result-the-town-has-had-31-for-sorting-i-1ry1ryjz.md)** for that. The migration number is 061; main's highest is 060.
- **UI inventory:** 18 web surfaces from packages/web/src, each marked goes, changes or new with its build step. Ones not in the 1:1 list:
  - town planning mode (`townPlan.ts` and `PlanToolbar`): goes;
  - the planning desk's create form: gets the Goal picker;
  - the Bank town map (`flow.ts`, pool tints): loses its meaning when pools go;
  - the Finance panel's Pools section;
  - map rendering and the minimap;
  - the Meeting panel;
  - the new kanban tabs.
- **Open questions are now 6:** owner powers, reorg lead time, skip-level with forks, confirming the "key below one session's cost can't run alone" rule, the empty-goal look, and long walks.

## What I need from you
Nothing needed. The 6 remaining questions and the [dc_io1ry1ryjz](../../note/2026-10/2026-10-30-every-key-result-the-town-has-had-31-for-sorting-i-1ry1ryjz.md) sort are already Mitchell's to answer.
