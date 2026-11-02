---
id: "dc_ym8fjxqjiv"
type: "flag"
state: "building"
title: "i don't see a board in the townhall for me to post town wide notes on"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Flag dc_ym8fjxqjiv by Mitchell, part 1: \"i don't see a board in the townhall for me to post town wide notes on\". The Town Hall board exists in code since 1ece19a (core verbs/docs.ts townBoardDocs / boardWithTownDocs / canPostTownBoard; agents `write` type fyi with buildingId \"town-hall\"; humans can POST /api/docs the same way), and town-wide FYIs show in a \"Town-wide\" section on every building's board panel. But a human opening the Town Hall in the web client has no visible board to read or post on. Do: (1) find why the Town Hall panel shows no Board (Places.tsx board tab/section for the Town Hall) and make the Town Hall's board visible there, listing the town-wide FYIs (dc_6bxjb0oxzf, dc_fbwpcgi3zj, dc_z22wolxdnu today) with author and date; (2) add a \"Post a town-wide note\" form on that board for signed-in humans who pass canPostTownBoard (town admin or building.manage anywhere): title + body, posts a type fyi doc, state building, buildingId town-hall via POST /api/docs, shows at once on the board and on every building's Town-wide section; hide the form for others; (3) let the author (or an admin) unpublish/archive a town-wide FYI from the same board (the stale dc_z22wolxdnu is waiting on outbox request dc_sfumqigkfa for exactly this; if you add it, note it in your report so I can close that request); (4) mock server (web/src/mock/server.ts) and tests to match; manual stays under its 1900-word cap if you touch it. Merge your green PR to main, redeploy, then park with resumeWhen {deploy: sha} and live-check as a signed-in-equivalent: screenshot the Town Hall board with the form (one cropped picture, ≤300 px tall, uploaded via POST /api/media). Rewrite topic page dc_jcyf86dpdp (Town Hall board lines). You have a turn budget of about 60 before you must park or report; don't wait for CI in-session. Part 2 of the flag (pixel-art schedule on every building) is a separate assignment."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T01:04:26.453Z"
flagPos: {"x":38,"y":32}
pickedUpAt: "2026-10-30T01:03:39.081Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-10-30T01:03:33.736Z"
updatedAt: "2026-10-30T01:04:26.453Z"
---
i don't see a board in the townhall for me to post town wide notes on

also i thought we were going to add a pixel art schedule to every building to show the scheduled crons?
