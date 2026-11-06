---
id: "dc_t0qjvmx9gf"
type: "report"
state: "building"
title: "Bulletin board for humans in the town square: PR #357 open, check green locally; parked on CI to merge"
authorId: "ag_dvdexjr16z"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_52njv3shp8","dc_8fxokwfk75"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/357"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Bulletin board PR #357 built; its continuation (as_2jewwqzjpl → as_4mloscwfi9, waiting on #357's CI at 96f6da4) merges it. Goes into rollup 49 once live; Mitchell's check there is to post a real note signed in."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T19:26:39.309Z"
sessionId: "se_6oysz6pxar"
assignmentId: "as_ge87lu7nu4"
costUsd: 4.444059200000001
tokens: 222203
turns: 91
createdAt: "2026-11-05T19:18:20.030Z"
updatedAt: "2026-11-05T19:26:39.309Z"
---
## What I did
I built Mitchell's flag [dc_52njv3shp8](../../flag/2026-11/2026-11-05-can-i-get-a-bulletin-board-outside-the-town-hall-f-njv3shp8.md): a free-standing bulletin board for humans in the town square, outside the Town Hall. It is in PR https://github.com/mitchellgordon95/muster-town/pull/357, a draft with head 0fee62b7, and main is merged into it. `npm run check` passed locally (docs, deadcode, typecheck, all tests; 10m29s). After merging main I ran typecheck again and it passed. I'm parked until the PR's CI finishes, and the continuation merges it. It is not merged and not live yet.

## Findings
- **Map:** a new tile `TILE.BULLETIN` (36) and a new place `bulletin:town` (kind `bulletin`).
  - On the default fountain map it stands on the square, 3 tiles left of the Town Hall door and just below the left flower bed. The fountain is below it. You read it from the tile in front of it.
  - On the tree and radial maps, `bulletinSpot` in layout.ts puts it on the grass nearest the door. On the live tree fixture that is about 10 tiles away, beside the main street.
  - Layouts are rebuilt from the goal tree, so every collective, hosted ones included, gets it without a migration.
  - The new pixel art (`drawBulletin`) is a cork board on two posts under a small red roof, with notes pinned on it.
- **Picture:** mf_lgfb1dvxxd, 672×288. It is the real fountain map of the live tree fixture, drawn by the web's own map renderer.
- **Notes:** a new doc type `bulletin`, kept in core `bulletin.ts`. Notes belong to no building, so they appear on no board and in no filing cabinet.
  - `GET /api/bulletin`: anyone can read the notes, guests included, newest first.
  - `POST /api/bulletin`: any signed-in human can post a note. Agents get 403, and the `write` verb refuses the type.
  - `POST /api/bulletin/:id/take-down`: the note's author or a town admin takes it down. It goes back to the author's drafts.
  - A signed-in visitor who hasn't been let in yet still gets 403, from the existing join gate.
- **Panel:** pressing E at the board says "Read the bulletin board" and opens a panel listing the notes. Signed-in humans see a "Post a note" form with a "Pin it" button. The author or an admin sees "Take down".
- **Agents and manual:** agents' `look` lists the board. The manual has one new line under "Outside on the square". I trimmed other wording to fit, and it is now at 1,898 of its 1,900-word cap.
- **Tests:** core `test/bulletin.test.ts`, `map-shapes.test.ts` (the board is placed and reachable in every map shape), server `test/bulletin.test.ts`, web `test/bulletin.test.tsx`.
- **Not tested:** nobody has posted a real note while signed in on muster.town. Desks have no GitHub sign-in, so that needs a human.
- **Topic page:** [dc_8fxokwfk75](../../wiki/2026-11/2026-11-05-bulletin-board-in-the-town-square-flag-dc-52njv3sh-xokwfk75.md) has the design, the file paths, and how to render the real map headless for pictures.

## What I need from you
Nothing needed.
