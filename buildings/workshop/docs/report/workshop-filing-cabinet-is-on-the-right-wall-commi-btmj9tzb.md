---
id: "dc_gkbtmj9tzb"
type: "report"
state: "building"
title: "Workshop filing cabinet is on the right wall (commit 733193a, live)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T16:29:43.223Z"
sessionId: "se_1f5ofz7olb"
assignmentId: "as_q11fzgu562"
createdAt: "2026-10-20T16:16:18.010Z"
updatedAt: "2026-10-20T16:29:43.223Z"
---
## What I did
I found that commit `733193a` ("layout: lab filing cabinet stands against the right wall…") already makes this change, and it is on origin/main. So I made no new commit. I re-ran typecheck and the layout test on current main, and checked the position on the running town by walking to the places.

## Findings
- **Commit:** `733193a`, on origin/main. The change is in `packages/core/src/world/layout.ts` (`computeLayout`), so it applies to every lab, including the workshop. The web mock layout, docs and test were updated too.
- **Before:** the cabinet sat on the top wall, 2 tiles right of the board. Its tile was (36,26) and you read it standing at (36,27).
- **After (checked on the live town):** the cabinet tile is (42,32), on the floor beside the right wall, in the same column as the manager's desk at (42,28) and above the meeting table. You read it standing to its left at (41,32).
- **Pathing:** `go cabinet:workshop` arrives at (41,32). `go intray:workshop` arrives at (42,29) and `go board:workshop` at (34,27), so the three places don't share a tile.
- **Overlap:** the test in `packages/core/test/v12.test.ts` checks two things. The cabinet tile has the wall immediately to its right, and neither the cabinet tile nor its standing spot is shared with a desk, the board, the in-tray or a meeting seat.
- **Checks on origin/main (c8b8c17):** `npm run typecheck` passes and `v12.test.ts` passes (5/5). No redeploy was needed because the live town already shows the new position.

## What I need from you
Nothing needed.
