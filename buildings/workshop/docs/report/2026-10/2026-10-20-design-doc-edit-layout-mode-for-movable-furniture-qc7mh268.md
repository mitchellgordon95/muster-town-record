---
id: "dc_c6qc7mh268"
type: "report"
state: "building"
title: "Design doc: \"Edit layout\" mode for movable furniture (dc_7sweg4w78o)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "only humans\ntown hall can be editable, sure\nnot sure about what you mean by desk blocks. just do something reasonable for now"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T16:33:01.027Z"
sessionId: "se_q86lj2k2rt"
assignmentId: "as_hspsqyam78"
costUsd: 0.5508420999999999
tokens: 16542
turns: 15
createdAt: "2026-10-20T16:08:10.334Z"
updatedAt: "2026-10-20T16:33:01.027Z"
---
## What I did
I read the layout code first: `layout.ts` (`computeLayout`, `TOWN_HALL_FIXTURES`), `map.ts` (`rebuild`), `movement.ts`, the permissions/roles and how the web client handles layout changes (`state.ts`). Then I wrote the design doc **[dc_7sweg4w78o](../../article/2026-10/2026-10-20-design-edit-layout-mode-for-movable-furniture-weg4w78o.md)** (an article, filed in the Workshop cabinet). It's about a page, with an ASCII sketch and a flow. No code changed and nothing was committed.

## Findings
- **Today:** every piece of furniture is hard-coded as an offset from the building's lot and recomputed on every `rebuild()`. No positions are stored.
- **Who and how:**
  - Humans with `building.manage` can edit their building; only the admin can edit the Town Hall. It's a web/REST action, not an MCP verb.
  - An **Edit layout** button in the building panel opens a draft that exists only in the browser: a grid over the room, pieces that snap tile by tile, **R** to rotate (floor pieces turn, wall pieces move to another wall), and a green/red preview of legal spots.
  - Save sends the whole draft in one call; Esc throws it away.
- **Rules:** one shared function, `validateLayout`, drives the preview and the server check on Save (the server's answer is final):
  - nothing on the door or the tile just inside it;
  - no overlaps;
  - stand tiles walkable and unique;
  - a flood fill from the door reaches every stand tile and at least 2 meeting seats.
- **Agents when a layout is saved:**
  - Bodies at an old stand tile move instantly to the new one, and place ids don't change, so agents' prompts aren't affected.
  - Bodies on a newly blocked tile move to the nearest free tile.
  - Walking agents get their route re-planned.
  - People in a meeting are re-seated through `standingTile()`.
- **Persistence:** a new optional JSON field `Building.furniture` stores only the moved pieces, relative to the lot. It lives in SQLite next to `lot`, so it survives redeploys, and it goes into the export. The seed never writes it. If the lot changes, any piece that becomes illegal goes back to its default.
- **Undo/reset:** Ctrl+Z works while editing, plus Reset piece and Reset room. After a save, "Revert last layout change" uses the previous layout kept in the `building.layout` event.
- The doc ends with 3 open questions for Mitchell:
  1. Should agents also get a move verb?
  2. Can the Town Hall be edited at all?
  3. Do desks move one at a time or as one block?

## What I need from you
Mitchell to answer the 3 open questions at the end of [dc_7sweg4w78o](../../article/2026-10/2026-10-20-design-edit-layout-mode-for-movable-furniture-weg4w78o.md) before anyone builds this.

## Reply from Mitchell (2026-10-20 12:33)

only humans
town hall can be editable, sure
not sure about what you mean by desk blocks. just do something reasonable for now

