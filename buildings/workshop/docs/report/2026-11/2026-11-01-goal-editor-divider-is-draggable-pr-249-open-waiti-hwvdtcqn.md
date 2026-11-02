---
id: "dc_8ghwvdtcqn"
type: "report"
state: "building"
title: "Goal editor divider is draggable: PR #249 open, waiting on CI"
authorId: "ag_gi5e74j7p5"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_bc67e2sw7z","dc_hsq0e5a587"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/249"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Continuation as_1t4nt9owgb already waiting on {pr: 249}: merge main again, merge if green, redeploy, guest-check the drag, add the Shipped candidate to dc_7lpbltjy1j."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T02:26:59.588Z"
sessionId: "se_a4g6sosrxf"
assignmentId: "as_6dd9f61ig2"
costUsd: 1.1213000999999998
tokens: 56065
turns: 25
createdAt: "2026-11-01T02:25:56.158Z"
updatedAt: "2026-11-01T02:26:59.588Z"
---
## What I did
I built Mitchell's flag [dc_bc67e2sw7z](../../flag/2026-11/2026-11-01-nit-i-want-to-be-able-to-resize-the-partition-in-t-67e2sw7z.md): you can now drag the line between the goal canvas and the detail pane in the goal tree editor. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/249. Main was merged in first. `npm run check -- --fast` passed (54 web tests) and `npm run check -- deadcode` passed. I have not tried it in a browser yet; the guest live check comes after the deploy.

## Findings
- **How it works:** `GeDivider` in `packages/web/src/panels/panelResize.tsx` copies the pattern of the side panel's `PanelResizer`. It sits in a zero-width middle grid column of `.ge-body`.
  - Drag sets the detail width with `geDetailWidth`. The detail pane keeps at least 320 px and the canvas at least 360 px.
  - Arrow keys move it 40 px. Double-click or Home goes back to the 60/40 default.
- **Remembered width:** it is saved in localStorage under `musterTown.goalEditor.detailWidth`. The CSS clamps it again (`.ge-body.sized`: `max(320px, min(var(--ge-detail), calc(100% - 360px)))`), so a smaller window still keeps both minimums.
- **Small screens:** the divider is hidden at 760 px and narrower, where the editor stacks the two panes.
- **Fit after a resize:** `GoalCanvas.tsx` now refits the tree when its pane changes size, as long as the view is still the last Fit. A manual pan or zoom is left alone, and the Fit button always uses the current pane size.
- **Tests:** `packages/web/test/panelResize.test.tsx` checks the handle's markup, that a drag gives the right width with both minimums, and that the width is saved and reset. There is no DOM test environment in packages/web, so a real pointer drag is not tested; the live check will cover it.
- **Docs:** item 3 in `docs/goals.md`, and a line in `docs/log.md`. The topic page [dc_hsq0e5a587](../../wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md) is updated.
- **Plan for the continuation (parked on {pr: 249}):** merge main again, merge if green, redeploy, then do a guest check in headless Chromium:
  - Open `openPanel("goals")` and drag `.ge-divider`. The `.ge-detail` width should change and stay at least 320 px.
  - Reload: the width should still be there.
  - After the resize, Fit should still show every box.
  - Then add a Shipped candidate to [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md).

## What I need from you
Nothing needed.
