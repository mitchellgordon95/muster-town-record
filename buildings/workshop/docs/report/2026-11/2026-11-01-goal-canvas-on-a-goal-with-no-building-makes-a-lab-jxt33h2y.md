---
id: "dc_i5jxt33h2y"
type: "report"
state: "building"
title: "Goal canvas: + on a goal with no building makes a lab there (1 desk, manager); PR #248 open, waiting on CI"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_jy52erwf1w","dc_hsq0e5a587","dc_7lpbltjy1j"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/248"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #248 parked on CI; its continuation merges, redeploys and guest-checks. Mitchell tries the + himself (rollup 37 item 11 \"Your call\")."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T02:21:52.830Z"
sessionId: "se_wy8ch7sfia"
assignmentId: "as_6oeaiigq5d"
costUsd: 3.53776455
tokens: 176888
turns: 42
createdAt: "2026-11-01T02:21:13.776Z"
updatedAt: "2026-11-01T02:21:52.830Z"
---
## What I did
Built the + from 1:1 mt_n25udpflus decision 3 (buildings are a thin layer on goals) in `packages/web/src/panels/GoalCanvas.tsx`. An admin (town.manage_buildings) sees a + beside the desks tag of an active goal with no building attached. Pressing it calls `POST /api/buildings { goalId, headcount: 1 }`, the same path as the Planning desk's New building: core `createBuilding` names the lab after the goal's short text and seeds its manager. On success it toasts "<name> is under construction: 1 desk and its manager", reloads the tree and selects the goal, so the usual − / + desk steps show for the new building. The button reads "…" and is disabled while the request runs; an error toasts (a non-admin with town.manage_buildings but no goals.edit on that goal gets the server's 403). The canvas prop `onMoved` is now `onChanged` (a move or a new building both reload). The mock's `createBuilding` now honours `headcount` so the demo makes a 1-desk building.

Test: web `test/goalTree.test.tsx` renders the canvas as an admin (+ on goals with no building and on the root, − / + on the attached Workshop, nothing on the retired goal) and as a guest (neither). Docs: `docs/goals.md` canvas paragraph, `docs/log.md`. Pages rewritten: [dc_hsq0e5a587](../../wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md) (goal tree editor UX) and [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) (Rollup 37 materials, item 11).

## Findings
- PR #248 (draft): https://github.com/mitchellgordon95/muster-town/pull/248, head 4c261bb, base main (branch merged with main first, already up to date). `npm run check --fast` green locally: docs 1 s, typecheck 12 s, 135 web tests in 25 files.
- No core or server change was needed: `ops.createBuilding` already seeds a manager (starterResidents) and sizes the lot from the headcount, so headcount 1 gives a one-desk lab.
- Not exercised live: the + needs a signed-in admin, so the guest live check after deploy can only confirm the goal tree still renders. Mitchell can try it by pressing + on any goal box with no building (for example a goal under Steer with "0 desks").
- Kelly's FYI (ms_w6zh0qni1x, pre-refactor strings in GoalTreePanel/PlanningPanel/BuildingPanel/GoalsTab) and Cleo's lag sample (ms_a6juproo21) both said nothing needed; not taken up here.

## What I need from you
Nothing needed.
