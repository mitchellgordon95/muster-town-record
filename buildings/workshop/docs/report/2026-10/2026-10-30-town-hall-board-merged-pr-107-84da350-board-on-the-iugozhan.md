---
id: "dc_1tiugozhan"
type: "report"
state: "building"
title: "Town Hall board merged (PR #107 = 84da350): board on the wall, Post a town-wide note, Take off the board; live check parked"
authorId: "ag_q22579imgf"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ym8fjxqjiv","dc_jcyf86dpdp","dc_sfumqigkfa"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/107"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #107 = 84da350 (Town Hall board place at lot (8,0), Post a town-wide note for admins/managers, Take off the board via POST /api/docs/:id/unpublish; no migration, no Bank change). The live check is already parked as as_pg4ob3zyf0 on deploy 84da350; nothing more to queue. Folds into rollup 31 Shipped \"Mitchell's flag: Town Hall board + schedule object\" together with as_h9qzlnc8p5. Outbox dc_sfumqigkfa stays open: once live, Mitchell presses Take off the board on dc_z22wolxdnu."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T01:12:55.711Z"
sessionId: "se_z3f4308yes"
assignmentId: "as_3tkqzuejle"
costUsd: 2.5143229000000007
tokens: 125716
turns: 59
createdAt: "2026-10-30T01:12:44.224Z"
updatedAt: "2026-10-30T01:12:55.711Z"
---
## What I did
Fixed part 1 of Mitchell's flag [dc_ym8fjxqjiv](../../flag/2026-10/2026-10-30-i-don-t-see-a-board-in-the-townhall-for-me-to-post-8fjxqjiv.md): PR https://github.com/mitchellgordon95/muster-town/pull/107, merged to main as **84da350**, redeploy queued. Local typecheck is green, and so are the web (143), server (219) and relevant core tests. I merged before CI finished, as the assignment said. Not live-checked yet: this report parks on deploy 84da350.

## Findings
- **Why there was no board:** the Town Hall's furniture list (core/world/furniture.ts) had no `board` piece, so no `board:town-hall` place existed. The board panel code was there, but nothing on the map opened it.
- **Fix:**
  - The Town Hall now has a wall board at lot (8,0), so its standing tile is (8,1) and it moves nothing else. The live Town Hall's furniture overrides were `{}`.
  - Its place `board:town-hall` shows in every agent's `look`.
  - The Town Hall board panel lists the town-wide FYIs, each with its author and how long ago it was posted.
  - **Post a town-wide note** (title + body) sends a type `fyi`, state `building`, buildingId `town-hall` doc through POST /api/docs. Only admins and people who can manage any building see it.
  - **Take off the board** is shown to a note's author or an admin. It uses the new `POST /api/docs/:id/unpublish` (core `unpublishTownFyi`), which moves the note back into its author's drafts. Nothing is deleted, and it disappears from every building's Town-wide section.
  - No migration and no Bank change.
- **Tests and mock:** two new tests in core/test/town-board.test.ts and two in web/test/townBoard.test.tsx. The mock server has the new board place, a sample town-wide FYI, and an unpublish route; writeDoc now keeps buildingId. Manual is at 1,896 words (cap 1,900).
- **Outbox [dc_sfumqigkfa](../../../../../town-hall/outbox/2026-10/2026-10-29-unpublish-the-stale-town-wide-fyi-dc-z22wolxdnu-re-umqigkfa.md):** once 84da350 is live, the author of dc_z22wolxdnu (Pix) or an admin can press "Take off the board" on it. No agent verb does this; the button is for humans. So that request can close once a human presses it.
- Topic page [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md) rewritten.
- **Next session plan:** confirm /api/health shows commit 84da350. Then open the Town Hall board in a headless browser signed in as a fake admin, using the method in [dc_d0hw7o8tp8](../../wiki/2026-10/2026-10-29-town-planning-side-bar-hw7o8tp8.md). Check that it lists dc_6bxjb0oxzf, dc_fbwpcgi3zj and dc_z22wolxdnu and shows the form. Take one cropped screenshot (≤300 px tall), upload it with POST /api/media, and mark [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md) live-checked.

## What I need from you
Nothing needed.
