---
id: "dc_04q4h8s229"
type: "flag"
state: "building"
title: "nit: can i get a read / unread tracker for the bulletin board by user? and then a red badge for unreads"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_04q4h8s229, verbatim: \"nit: can i get a read / unread tracker for the bulletin board by user? and then a red badge for unreads\". Build it, one PR, lane directed.\n\nWhat exists (main 565a075): the bulletin board is docs of type \"bulletin\", state \"building\", no building (packages/core/src/bulletin.ts: bulletinNotes / postBulletin / takeDownBulletin); routes GET/POST /api/bulletin and POST /api/bulletin/:id/take-down (packages/server/src/routes/docs.ts:77-83); the panel is BulletinPanel in packages/web/src/panels/Places.tsx:829 (opens a note via DocView); the map place is bulletin:town (web/src/map/world.ts, renderer.ts). There is NO per-user read state for any doc today (only inbox messages have unread, verbs/social.ts:199). Map badges already exist: drawBadge (map/overlay.ts:185) is used for in-tray counts and the outbox counter (renderer.ts:752-766); copy that pattern.\n\nBuild:\n1. Server: an additive migration with a small table, e.g. bulletin_reads(userId, docId, readAt) keyed per signed-in HUMAN (world.holderOf(me).kind === \"user\"; \"by user\" is what Mitchell asked for: agents and guests get no tracking). POST /api/bulletin/:id/read marks one note read; GET /api/bulletin returns, for a signed-in human, `readAt` (or `unread: true/false`) per note plus an `unread` count; guests get the notes with no flags. A note posted by the user counts as read by them. Taking a note down removes nothing (keep reads; a re-pinned note after edits can stay read: simplest rule, say which you chose).\n2. Panel: BulletinPanel marks a note read when it is opened (the DocView back-and-forth at Places.tsx:836), shows an unread dot/“new” mark on unread rows, and a \"Mark all read\" link only if cheap. Signed-out: nothing changes.\n3. Map: a red count badge on the bulletin board (bulletin:town) for a signed-in human with unread notes, same drawBadge tone \"bad\" as the in-tray badges (renderer.ts:752-760); the count comes from whatever state the HUD already polls (check state.ts / api.ts for the world/me snapshot the renderer reads so it doesn't add a new poll; one extra field on the existing /api/bulletin fetch or the me/notices call is fine, say which). No badge for guests or when 0.\n4. Mock (packages/web/src/mock/server.ts) gets the same so the Playwright/vitest tests run; add tests next to packages/server/test/bulletin.test.ts and packages/web/test/bulletin.test.tsx. `npm run check:css` stays exit 0; new colour/size only through tokens.\nOpen the PR, park on {pr: N}, merge when green, do NOT call redeploy (CI deploys main; FYI dc_vzqoh7ppen), park on {deploy: <merge sha>}, verify on live signed in with the test account if MUSTER_TEST_GH_TOKEN is in the Town Hall secrets (FYI dc_ia2hybtuax), else as far as the mock and a guest view go, and say so. One crop (≤300 px tall) of the badge on the map or the unread dot in the panel for the rollup. Report in the usual three sections; rewrite/start a topic page \"Bulletin board\" with the read-state rule and the ids."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-05T20:16:46.109Z"
flagPos: {"x":73,"y":17}
pickedUpAt: "2026-11-05T20:15:59.750Z"
pickedUpBy: "ag_s1kuuuo54b"
createdAt: "2026-11-05T20:15:49.357Z"
updatedAt: "2026-11-05T20:16:46.109Z"
---
nit: can i get a read / unread tracker for the bulletin board by user? and then a red badge for unreads
