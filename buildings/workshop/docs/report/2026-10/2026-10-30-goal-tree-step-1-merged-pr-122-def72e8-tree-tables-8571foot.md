---
id: "dc_gz8571foot"
type: "report"
state: "building"
title: "Goal tree step 1 merged (PR #122, def72e8): tree tables, owners, attachment, Goals.inScope; live check parked"
authorId: "ag_j81x2uz660"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 merged (PR #122, def72e8) and live-checked by Pix 1 in dc_f3ue446bxn; the parked live check is covered. Step 2 queued separately."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T21:33:10.098Z"
sessionId: "se_bq4ulslc0a"
assignmentId: "as_6zx9zmtvdo"
costUsd: 7.288847200000002
tokens: 364442
turns: 111
createdAt: "2026-10-30T21:00:04.582Z"
updatedAt: "2026-10-30T21:33:10.098Z"
---
## What I did
- Merged the design doc first: PR #116 into main (517d1d2). Commit 8aa0f16 marks the doc approved and adds Mitchell's line that donor emails via Resend come "eventually, not now".
- Built step 1 on a branch off main and opened PR #122 (https://github.com/mitchellgordon95/muster-town/pull/122). Local `npm run check` passed (6m02s) and CI passed (2m14s). I checked again just before merging that main's highest migration was still 060, then merged it as **def72e8** and queued the redeploy. **def72e8 should be live.** I have not checked it live yet; this session is parked until the deploy lands, and the continuation does the live check.

## Findings
What step 1 shipped (docs/goals.md, "Build order" step 1, plus the UI inventory rows marked step 1):
- **Migration 061** only adds; it removes nothing.
  - New tables: `goals`, `goal_proposals`, `goal_changes`.
  - The root goal `gl_town` holds the town goal, with `gl_fund`, `gl_join` and `gl_trust` under it as placeholders.
  - Every lab gets its own goal `gl_<buildingId>` under the root and is attached to it. The Town Hall is attached to the root.
  - Objectives become goals with the same ids. Each key result gets a `goalId` (its objective, else its building's goal), and met or missed ones are archived.
  - `goals.edit` is added to the admin role. Grants are untouched.
- **`Goals` service** (`packages/core/src/goals.ts`):
  - the tree, and `inScope`: is a key result open and under the building's attached goal;
  - edit, move, and retire (a retired goal's open key results and buildings move to a sibling, or retiring is refused);
  - attach: a building always has exactly one goal, and clearing it is refused;
  - human owners, inherited down the tree: an owner edits, funds grants and marks key results met or missed only within their part of the tree;
  - `route`, which says whose in-tray an item belongs to;
  - proposals: add a goal or key result, edit, move, retire, promote.
- **Scope switch:** grant proposals, exploration and directed work now must name an open key result under the building's attached goal, instead of "the building's own key result". A building now counts as blocked when no open key result sits under its attached goal.
- **New routes** in `packages/server/src/routes/goals.ts`. **New verbs:** `propose_goal` and `propose_key_result`, limited to a building's manager, its forks, and humans. The desk brief now shows "Attached to: path (owner)" and the goals under it with their open key results.
- **Web:** a Goal picker on the planning desk's create form (default: the root), and an **Attached to** section in building Settings.
- **Kept for now, deliberately:** `set_objective` and `set_key_result` still write directly, and their changes are copied into the tree. Accepting proposals has no UI until steps 3 and 4, and removing them now would leave managers unable to add key results.
- **Tests:** `packages/core/test/goals.test.ts` has 8 tests: scope, owners and routing, a building can't be left without a goal, retire, proposals, and a migration test showing every key result keeps its id, status and goal. I adjusted two existing tests for the new scope rule and brief format. The invariants docs, `architecture.md`, `log.md` and the step-1 "Built" note in `docs/goals.md` are updated.
- **Expected live (as the doc predicts):** 16 goals. Bank Transparency (all its key results archived) and UI / UX (no key results) become blocked, and each manager is woken once to propose a key result.
- **One thing to know:** a new building attached to the root can work on any open key result in the town, since the whole tree is under the root.
- The topic page "Town-level goal tree (design)" ([dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md)) is rewritten with this state.

## What I need from you
Nothing needed.
