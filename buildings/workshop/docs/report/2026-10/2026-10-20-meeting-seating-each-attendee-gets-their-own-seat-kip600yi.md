---
id: "dc_zokip600yi"
type: "report"
state: "building"
title: "Meeting seating: each attendee gets their own seat at the table (draft PR #26)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "mrege"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:53:36.186Z"
sessionId: "se_fzhun769nr"
assignmentId: "as_gh3fvv9dtc"
costUsd: 0.5520824999999999
tokens: 25992
turns: 19
createdAt: "2026-10-20T03:48:29.510Z"
updatedAt: "2026-10-20T03:53:36.186Z"
---
## What I did
Changed the code so people walking to a meeting room each take their own tile around the table instead of all stacking on one tile. Opened draft PR https://github.com/mitchellgordon95/agent-town/pull/26.

## Findings
- **How seats work:** every walkable tile touching a meeting table now counts as a seat (`seatsAround` in `packages/core/src/world/layout.ts`). The room's original tile is the first seat. Seat counts are checked by the test only as "at least 6" for each table; the exact numbers are below.
  - Lab table: 3 table tiles, so up to 8 seats (6 above and below, 1 at each end).
  - Town Hall table: 4 table tiles, so up to 10 seats.
- **Choosing a seat:** `World.standingTile` picks the first seat that no other body is standing on or walking to. Because seats being walked to count as taken, people arriving at the same time don't collide. Someone who is already seated keeps their seat. If every seat is taken, the person falls back to the room's original tile, so stacking only starts after about 8 people in a lab.
- **Who uses it:** both the `go` verb and the runtime's step that gathers attendees for discussion (`packages/runtime/src/meetings.ts`).
- **Place lookup:** `placeAt` now maps any seat back to its meeting room, so `go` still reports `place: meeting-room:*` for a seat at the far end of the table.
- **Docs:** updated `docs/architecture.md` and added a line to `docs/log.md`.
- **Checks:** `npm run typecheck` is clean and `npm test` passes in every package (core: 79 tests). I added one layout test: 4 visitors walk to the same room at once and end up on 4 different seats, and walking there again keeps the same seat. I didn't look at it in a browser.

## What I need from you
Review and merge PR #26.

## Reply from Mitchell (2026-10-19 23:53)

mrege

