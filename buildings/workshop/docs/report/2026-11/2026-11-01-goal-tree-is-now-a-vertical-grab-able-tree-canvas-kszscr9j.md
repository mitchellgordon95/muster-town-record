---
id: "dc_agkszscr9j"
type: "report"
state: "building"
title: "Goal tree is now a vertical, grab-able tree canvas (PR #237); parked on CI"
authorId: "ag_m29nyh4yog"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #237 (193e19c) built per mt_cyd2t5ioob D4-D6 with three screenshot rounds; continuation as_v1egdkthgf already waits on {pr:237} (merge, redeploy, set root captain, guest check of the canvas). Nothing more to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T01:29:17.019Z"
sessionId: "se_5cyuwx11sf"
assignmentId: "as_4n8tzh77hd"
costUsd: 4.425479700000001
tokens: 222915
turns: 56
createdAt: "2026-11-01T01:26:40.002Z"
updatedAt: "2026-11-01T01:29:17.019Z"
---
## What I did
Built 1:1 mt_cyd2t5ioob decisions 4, 5 and 6 into one PR, [#237](https://github.com/mitchellgordon95/muster-town/pull/237) (commit 193e19c). The goal tree sheet now shows a textbook top-down tree canvas instead of the indented outline. The PR also adds desks −/+ on each box, lets a headcount go below the occupied desks, and adds a captain badge. `npm run check` passed locally (docs, dead code, typecheck, all test files, 7m17s). I took three rounds of screenshots in mock mode and fixed what looked off each time: building tags clipped on the root, too much empty space in leaf boxes, the drag ghost covering its drop target. Topic page [dc_hsq0e5a587](../../wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md) is rewritten. Parked on `{pr: 237}`.

## Findings
![Goal tree canvas (mock): root at top with Mitchell's captain badge and per-building desks −/+, Fund/Join/Trust below, their goals a row further down](/api/media/mf_juswc644e6.png)

- **Canvas** (`GoalCanvas.tsx`, layout in `goalCanvas.ts`):
  - **Layout:** root at the top, each goal's children in a row beneath it, joined by elbow lines. Each parent is centred over its children's row, so subtrees never overlap.
  - **Pan and zoom:** drag empty canvas to pan. Wheel, pinch or −/+ to zoom (25–200%). Fit, `0` or a double-click on empty canvas frames the whole tree. A `?goal=` link centres that box.
  - **Selecting and collapsing:** clicking a box selects it, and the detail pane is unchanged. ▾/▸ under a box collapses its subtree and shows how many goals are hidden.
  - **Moving:** drag a box onto another, confirm "Move X under Y?", and it saves with the same rule as the Move form.
  - **Keys:** arrows walk the tree (up = parent, down = first child, left/right = next box in the row). Enter jumps to the detail.
  - **Checked in headless Chromium against the mock:** pan, drag-to-move with a green target and the confirm (drag picture: mf_gxtaxwd2jb), collapse, click-select, arrow keys, and the deep link centring at 100%. No page errors.
  - **Removed:** the outline and its "Key results" toggle. Key results now show only in the detail.
- **Desks −/+ (decision 5):**
  - Each attached building gets a row "Name · N" on its box. Admins see − and + on hover or selection. The change shows at once and is reverted with a toast if the server refuses it.
  - In core, a headcount below the occupied desks is now accepted. It only stops new forks from taking a desk; running forks keep theirs.
  - A lab keeps its lot and desk furniture up to its highest occupied desk, and shrinks as those desks free, so an occupied desk is never dropped. Town Hall is unaffected.
  - Tests are in core `furniture.test.ts`.
- **Captain badge (decision 6):** a 👤 name badge appears only on goals with their own captain.
  - Live, the root has no captain (`GET /api/goals`, server time 01:14Z).
  - When I tried to set it to Mitchell (`us_1la74k332n`), the server refused with "The town admins captain the root." That is a rule in the code, not a permission problem.
  - The PR changes the rule so only a town-wide admin can name the root's captain. Test in core `goals.test.ts`.
  - The mock's limits: it ignores desk changes and refuses moves, so live I could only check those up to the request.

**Plan for the continuation** (when PR #237's CI finishes):
1. If CI is green: merge, redeploy, and say which commit should be live.
2. Once that commit is live: set the root's captain to us_1la74k332n with PATCH /api/goals/gl_town. If my token can't, Mitchell does it in one click from the root's Captain tool.
3. Check the canvas on muster.town as a guest.

## What I need from you
Nothing needed.
