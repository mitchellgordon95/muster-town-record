---
id: "dc_svykbcny8n"
type: "wiki"
state: "building"
title: "Phone camera: two buildings after Watch first (kr_c3c7651d18)"
authorId: "ag_07syazuthn"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-04T01:48:33.647Z"
updatedAt: "2026-11-04T02:26:03.187Z"
---
State on live 7e439b3 (health commit at 2026-11-04 02:23 UTC; PR #295 merged: phone default zoom 2 when the canvas is under 600 CSS px or the pointer is coarse; leftInset 0 under the strip HUD; delight-walk taps Watch first).

Measured with scripts/delight-walk.mjs on live, guest, 2026-11-04 02:24–02:25 UTC:
- Phone 390×844 (2 runs): HUD cover after Watch first is 7% including the tap hint. 0 signs hidden, 0 cut, 0 overlaps. Zoom 2 is confirmed in the screenshot: desks are 64 px wide here against 96 px on the laptop. In view: UI / UX about 80% (west wall to the east desks; east wall off screen), its banner, the full street with lamps, and a door edge of the neighbour on the west. Not two whole buildings.
- Laptop 1280×800 (2 runs): 12% cover. At 1280×720 (1 run): 13%. 0 cut, 0 overlaps.
- Flake: in phone run 2 the agent moment returned "no agent on screen" while Teo 1 was visible. Run 1 reached it.

Why two buildings can't fit: a lot is 13–15 tiles (208–240 world px), so two lots plus the avenue come to about 480–512 world px. At 390 CSS px that needs zoom ≤ ~0.76. Rejected by the manager: zoom 0.75 (avatars about 9 px) and landing on the square (would undo renderer.ts:344-349). Rewording the check ("one whole building, its neighbour and a street") is Mitchell's call. No more phone camera work is planned.
Reports: [dc_4641dhux2c](../../report/2026-11/2026-11-04-phone-zoom-2-can-t-fit-two-whole-buildings-at-390-41dhux2c.md), [dc_c0uai2d5e8](../../report/2026-11/2026-11-04-phone-hud-on-live-0c5f5d9-12-8-cover-on-land-4-9-a-uai2d5e8.md), and this walk's report.
