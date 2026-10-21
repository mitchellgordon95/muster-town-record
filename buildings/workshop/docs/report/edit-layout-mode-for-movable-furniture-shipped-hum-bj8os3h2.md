---
id: "dc_sbbj8os3h2"
type: "report"
state: "building"
title: "Edit layout mode for movable furniture shipped (humans only, Town Hall included)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T17:54:08.600Z"
sessionId: "se_btcmjqqhb1"
assignmentId: "as_f0yh4izel3"
costUsd: 3.742538599999999
tokens: 7945058
turns: 82
createdAt: "2026-10-20T17:22:15.570Z"
updatedAt: "2026-10-20T17:54:08.600Z"
---
## What I did
I built the design from dc_7sweg4w78o using your answers:
- **Who:** only humans can edit.
- **Town Hall:** editable like any other building.
- **Desks:** for "desk blocks" I picked the simple option: each desk moves on its own.

It's committed straight to main as **96dae36** and the redeploy has started.

How I checked it:
- Typecheck is clean and all tests pass (251 across packages). That includes 6 new core tests and 1 new REST test.
- I drove the real web client in headless Chromium: dragged the board along the wall, nudged it somewhere illegal (it turned red with an error), used Ctrl+Z, saved, and confirmed what was stored. That run caught one preview bug, which is fixed.

## Findings
- **Using it:** open a building panel and click **Edit layout**. The button only shows if you can manage that building; for the Town Hall that means the admin.
  - The camera centres on the room and darkens the rest, and a grid appears.
  - Drag a piece, or click it and nudge it with the arrow keys. The spots where people stand show as dots.
  - The toolbar has Undo (Ctrl+Z), Reset piece, Reset room, Cancel (Esc) and Save.
  - Pieces that break a rule turn red with a message, and Save stays disabled until the room is legal.
- **Rules (checked by the server, which has the final word):**
  - Every piece stays inside the room; the board can only sit on a side or top wall.
  - Nothing goes on the door or the tile just inside it.
  - No two pieces overlap.
  - Every spot where people stand is free floor and belongs to only one piece.
  - Every one of those spots, and at least 2 seats at each meeting table, can be reached from the door.
- **What moves:**
  - Labs: each desk, the board, in-tray, cabinet, meeting table and plant.
  - Town Hall: mod station, donation box, planning desk, schedule board, library shelves, trophy cases, outbox counter, meeting table and the two plants.
- **Agents:**
  - Anyone standing at a place or meeting seat that moved goes to the new spot.
  - Anyone on a tile that is now blocked steps to the nearest free one.
  - Walks in progress are re-planned.
  - Place ids never change, so agents' prompts aren't affected.
  - Agent tokens get a 403 even if the agent manages the building.
- **Storage:** a new `Building.furniture` column (migration 013) keeps only the pieces that moved, so layouts survive redeploys and appear in the export. If a stored spot stops being legal (for example the lot grows), that piece goes back to its default spot.
- **Left out of this version:**
  - Rotating pieces (the board can still go on a side wall).
  - "Revert last layout change" (the previous layout is kept in the `building.layout` event).
  - The editor doesn't work in the mock web mode.
- I had to resolve a rebase conflict with Lena's Bank change: both of us had added a migration numbered 012, so mine is now 013.

## What I need from you
Nothing needed.
