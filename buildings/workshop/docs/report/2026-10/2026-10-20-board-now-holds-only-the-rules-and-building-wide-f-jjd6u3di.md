---
id: "dc_9bjjd6u3di"
type: "report"
state: "building"
title: "Board now holds only the rules and building-wide FYIs (new doc type `fyi`); pushed to main"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:44:06.072Z"
sessionId: "se_sttpfk3weh"
assignmentId: "as_ieu0olpq66"
costUsd: 0.6585312999999999
tokens: 888306
turns: 21
createdAt: "2026-10-20T04:42:23.033Z"
updatedAt: "2026-10-20T04:44:06.072Z"
---
## What I did
Changed what the board shows instead of deleting docs. There's a new doc type, `fyi`, and it's the only type that goes on a building's board, under the manager's standing rules. Every other published doc (notes, articles, reports, meeting notes) now goes in the filing cabinet. Pushed to main as commit 1dc7e6a, following your push-to-main rule.

## Findings
- **Your rule stays where it is.** It's the building's `rules` setting, which is pinned at the top of the board panel, not a board doc. Nothing touched it.
- **Clearing the 5 old board docs:** they are 1 article and 4 notes (Lena's token-budget design, Sage's docs gap list, Root's and my two "blocked" plans, my Chromium note). Under the new filter they drop off the board and show up in the filing cabinet. Nothing was deleted, and `search` still finds them. **The live server is still running the old code**: when I checked `board` just now, all 5 were still listed. They'll go once the server restarts on the new main.
- **Code changes:**
  - In the schema, `BOARD_TYPES = ["fyi"]` replaces `FILED_TYPES`. `boardDocs`, `cabinetDocs` and the web mock server now use it.
  - The descriptions for `write`, `board` and `promote` are reworded to match.
  - The board and cabinet panel subtitles are reworded.
- **What agents are now told:** post to the board (type "fyi") only when everyone in the building needs to know something. If only one colleague does, `tell` them. Anything else published goes in the filing cabinet.
- README, architecture.md and log.md are updated to match.
- **Checks:** `npm run typecheck` is clean. All tests pass: 86 in core plus 21, 31, 26 and 14 in the other packages. I updated two tests for the new rule: board shows FYIs only, notes go to the cabinet, and turning a note into an fyi pins it.

## What I need from you
Restart the server so the board clears.
