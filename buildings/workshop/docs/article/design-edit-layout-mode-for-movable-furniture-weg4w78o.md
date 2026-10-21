---
id: "dc_7sweg4w78o"
type: "article"
state: "building"
title: "Design: \"Edit layout\" mode for movable furniture"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["design","web","layout","furniture"]
createdAt: "2026-10-20T16:08:00.548Z"
updatedAt: "2026-10-20T16:08:00.548Z"
---
**Status:** proposal, no code yet. This is the general mechanism. Root's one-off move of the cabinet to the right wall doesn't depend on it.

## Where things stand
Every piece of furniture is hard-coded in `computeLayout` (`packages/core/src/world/layout.ts`), as offsets from the building's lot. Labs have desks (2 tiles wide, in rows of 3), a board and cabinet on the top wall, the manager's desk/in-tray at top-right, a meeting table at bottom-right and a plant. The Town Hall's pieces are listed in `TOWN_HALL_FIXTURES`. Each piece produces a **tile** (not walkable) plus a **place** (the walkable tile an agent stands on). `WorldMap.rebuild()` recomputes the grid and places whenever buildings or desks change. The web client already re-fetches the snapshot when a building's `lot` changes (`state.ts`). Positions aren't stored anywhere today. They are recomputed on every boot.

## Proposal

**Who can edit.** Humans who hold `building.manage` on that building: managers, or the admin. The Town Hall is admin-only. This is a REST/web action, not an MCP verb, so agents can't rearrange rooms in this first version (see Q1).

**Enter / leave.** The building panel gets an **Edit layout** button, shown only to people with permission. Pressing it:
1. Centres the camera on the lot and dims everything outside it.
2. Draws a tile grid over the room.
3. Pauses avatar movement and shows a toolbar: `Save · Undo · Reset piece · Reset room · Cancel`.

**Esc** or **Cancel** throws the draft away. **Save** sends the whole draft in one call. Agents keep working throughout, because the draft exists only on the client until Save.

**Select, drag, rotate.**
- Click a piece to select it. It gets an outline, and its stand tile shows as a small footprint marker.
- Drag it, and it snaps tile by tile. Arrow keys nudge it one tile.
- **R** rotates it:
  - Floor pieces (desk, in-tray desk, meeting table, donation box, planning desk) turn between horizontal and vertical. The stand tile moves to the "front" side.
  - Wall pieces (board, cabinet, schedule board) can only sit on wall tiles, so R moves them to another wall. The stand tile is always the floor tile just inside the wall.
- Each piece shows **green** where it can go and **red** where it can't. A red drop goes back to where the piece came from.

```
 Lab, edit mode (W wall, D door, ▒ desk, B board, C cabinet, M in-tray, T table, · stand tile)
 W W W W W B W C W W W W W W W
 W . . . . · . · . . . . . M W
 W ▒ ▒ . . ▒ ▒ . . ▒ ▒ . . · W     click → drag (snap) → R rotate
 W · . . . · . . . · . . . . W        │ green = legal, red = blocked
 W . . . . . . . . . . . . . W        ▼
 W . . . . . . . . . . . T T W     Save → server re-validates → rebuild()
 W . . . . . . . . . . . · . W        → agents re-seated/re-routed → snapshot
 W W W W W W W D W W W W W W W
```

**Rules.** One pure function, `validateLayout(lot, pieces) → errors[]`, used by the web client for the live green/red preview and by the server on Save. The server's result is final. A layout is legal when:
1. Footprints stay inside the lot: floor pieces on interior floor, wall pieces on non-corner wall tiles. No two pieces overlap.
2. Nothing sits on the door, or on the tile just inside the door.
3. Every stand tile is walkable, belongs to only one piece, and isn't part of another piece's footprint.
4. A flood fill from the door reaches every stand tile and at least 2 seats at the meeting table (`seatsAround`). Pieces may not wall off an area of the floor.

**Agents during a save.** Moving a body costs nothing, so the server handles it inside `rebuild()`:
- **Standing on an old stand tile** (sitting at their desk, reading the board): moved instantly to the new stand tile, with an `agents.pos` broadcast. "At my desk" stays true.
- **On a tile that is now blocked:** moved to the nearest walkable tile (BFS).
- **Walking:** `Movement` re-plans each route from the body's current tile. If the route was headed to a moved place, it goes to the new stand tile. If no route exists, the walk ends with `unreachable`, which the validation rules should prevent.
- **In a meeting:** re-seated through `standingTile()`.

Nobody needs to touch an agent's prompt, because places keep their ids and only `pos` changes. A `building.layout` event logs who moved what.

**Persistence.**
- A new optional field `Building.furniture` stores a map from piece key to `{x, y, rot}`, relative to the lot. Piece keys look like `board`, `cabinet`, `intray`, `meeting`, `plant`, `desk:0…n`, and for the Town Hall `donation`, `planning`, `schedule`, `mod-station`.
- It's stored as JSON on the `buildings` row, the way `lot` already is (`store.ts` json columns). It's written to the export's `building.json`.
- **Only moved pieces are stored.** `computeLayout` uses the stored position if there is one and the default otherwise. A redeploy only rebuilds code, and the SQLite data stays, so layouts survive it. `seedDefaults` never writes `furniture`.
- If a lot changes (headcount grows, so `assignLots` gives the building a bigger lot), `rebuild()` re-validates the stored positions. Any piece that is now illegal falls back to its default and gets a log line. New desks take their default spot, or the first legal free tile if that spot is taken.

**Undo / reset.**
- **While editing:** `Undo` (Ctrl+Z) steps back through a client-side stack of moves. `Reset piece` removes that piece's stored position, so it goes back to its default. `Reset room` clears `furniture` entirely (asks to confirm).
- **After saving:** the `building.layout` event payload keeps the previous layout. The panel then offers **Revert last layout change**, which re-applies that previous layout through the same Save path, with the same validation.

## Open questions for Mitchell
1. **Agents too?** Should manager agents get a `move_furniture` verb later, or stay humans-only?
2. **Town Hall:** is it editable at all, and by admin only? Or do we freeze it so the public square looks the same for everyone?
3. **Desks:** should they move one at a time, with their numbers fixed to `desk:n`? Or should we treat the desk block as one piece so headcount growth stays simple? Moving them one at a time makes it harder to place new desks when headcount grows.
