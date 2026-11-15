---
id: "dc_f3xcob2n9u"
type: "flag"
state: "building"
title: "move the fire hydrant from the corner to where the outbox is today, and remove the outbox town object from the UI"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag (dc_f3xcob2n9u, planted in the UI / UX just now): \"move the fire hydrant from the corner to where the outbox is today, and remove the outbox town object from the UI\". Do it in one PR.\n\nWhere things are in the code (main dc6a380): the Town Hall furniture is packages/core/src/world/furniture.ts: the hydrant at line 57 ({ key: \"hydrant\", at: { x: 15, y: 9 }, cells: one(TILE.HYDRANT), stands: [{ x: 0, y: -1 }] }) and the outbox counter at lines 66-67 ({ key: \"outbox\", at: { x: 2, y: 6 }, cells: row(2, TILE.COUNTER), stands: [{ x: 1, y: 1 }] }). The places come from packages/core/src/world/layout.ts: line 32 (hydrant { x: 15, y: 9 }, hydrantStand { x: 15, y: 8 }), line 154 (the hydrant place) and line 161 (the \"outbox\" place). The web side: packages/web/src/map/renderer.ts line 61 (the outbox place's verb) and lines 799-802 (the outbox badge drawn from state.outbox), packages/web/src/map/sprites.ts line 535 (the \"outbox\" IconKind), packages/web/src/panels/helpCard.ts lines 34 and 42, packages/web/src/panels/room.ts lines 22-29 (an outbox link already opens the decision queue), packages/web/src/state.ts (PanelKind \"outbox\" at line 23, the outbox count and outboxRev at lines 50-70), and the mock layout packages/web/src/mock/layout.ts lines 18, 67 and 97.\n\nWhat to do: (1) Move the hydrant to the outbox's spot: the hydrant tile where the outbox counter is today (around x 2-3, y 6 in Town Hall coordinates), with its stand tile below or beside it so a human can still walk to hydrant:<town hall> and the Secretary's rest (TOWN_HALL_RESTS in layout.ts line 21) still works. Keep the stream (packages/web/src/map/hydrant.ts, renderer.ts lines 563-581) pouring from the new spot toward the Secretary's desk. Check nothing else sits on that tile and that the old corner tile at (15, 9) becomes open floor. (2) Remove the outbox town object: drop the outbox furniture row, the \"outbox\" place, the outbox badge and its map icon, the help-card entry, and the dead PanelKind / outbox count plumbing if knip or typecheck says it is unused (keep what the decision queue still needs: a request is still a do ask there). Keep /api behaviour for requests unchanged: this is the map object only. (3) Update the tests that pin these positions: packages/web/test/hydrant.test.tsx line 15 (\"its tile right of the planning desk\"), packages/web/test/helpCard.test.ts line 40, packages/core/test/furniture.test.ts and layout.test.ts. (4) Run npm run check, open the PR, and if green squash-merge it (no redeploy; CI deploys). Note the move in a docs/log.d file, not docs/log.md. Report what a human sees on the live map: the hydrant at the outbox's old spot, no outbox counter, the corner tile open."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-15T20:55:31.001Z"
flagPos: {"x":75,"y":11}
pickedUpAt: "2026-11-15T20:54:48.605Z"
pickedUpBy: "ag_s1kuuuo54b"
createdAt: "2026-11-15T20:54:30.533Z"
updatedAt: "2026-11-15T20:55:31.001Z"
---
move the fire hydrant from the corner to where the outbox is today, and remove the outbox town object from the UI
