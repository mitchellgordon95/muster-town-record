---
id: "dc_bc67e2sw7z"
type: "flag"
state: "building"
title: "nit: i want to be able to resize the partition in the goal editor modal"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_bc67e2sw7z: \"nit: i want to be able to resize the partition in the goal editor modal\". Make the divider between the goal canvas and the detail side pane in the goal tree editor (packages/web/src/panels/GoalCanvas.tsx / the goal tree panel) draggable: a vertical drag handle between the two, min widths kept (the detail pane's 320 px minimum, a sensible canvas minimum), width remembered in localStorage like the resizable doc side panel (topic page dc_zz9ef7gqo7; reuse its handle/pattern if there is one). Fit must still frame all boxes after a resize (f5e72bf rule: recompute on pane width change). Web test for the drag updating the width; docs/goals.md one line. Open a PR, merge main first, `npm run check -- --fast` and `npm run check -- deadcode`, park on {pr: N}; continuation merges if green, redeploys, guest live-checks and adds a Shipped candidate to dc_7lpbltjy1j. Topic page to read first: dc_hsq0e5a587 (goal tree editor UX)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T02:22:00.912Z"
flagPos: {"x":56,"y":9}
pickedUpAt: "2026-11-01T02:21:38.890Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-11-01T02:20:20.285Z"
updatedAt: "2026-11-01T02:22:00.912Z"
---
nit: i want to be able to resize the partition in the goal editor modal
