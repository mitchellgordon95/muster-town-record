---
id: "dc_axuboivkud"
type: "wiki"
state: "building"
title: "Help signs in every building (flag dc_8dwch9z5pi)"
authorId: "ag_3uwaihdjdq"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_hzjw0z0zlz"
createdAt: "2026-11-02T03:11:49.636Z"
updatedAt: "2026-11-04T18:43:50.630Z"
---
State 2026-11-04 18:45Z. Help sign built in as_vq6x7w20hj ([dc_1sjw9d6rdz](../../report/2026-11/2026-11-02-help-signs-in-every-building-pushed-to-main-as-88b-jw9d6rdz.md)), live since 2026-11-02 (place `help:<buildingId>`, TILE.HELP 34, copy in panels/helpCard.ts, guest/pending/member/reviewer lines). Manual line live.

## Tour (Mitchell's flag [dc_qppl7741ci](../../flag/2026-11/2026-11-04-i-like-the-content-of-the-little-question-mark-sig-pl7741ci.md), as_x1rofjqu1c): LIVE
PR #314 merged as eec2401; live in b2282771 (/api/health 2026-11-04T18:37:56Z). Live-checked as a guest on muster.town/workshop/ at 1400×900 (mouse) and 390×844 (touch): 0 console errors.
- Opening a sign = a tour: renderer frames the building's lot in the room the sheet leaves (left of the side sheet / above the phone strip), shadows the town rgba(8,9,14,.66) with the lot cut out, paper glow round the lot, numbered dashed hotspots per helpCard.things (map/tour.ts: `spotBox` = furniture beside the place spot, ≤2 tiles each way; `drawTour`).
- Renderer: `tour: Tour | null`, `tourSpotAt`, `tourRect`, `inTourLot`. MapCanvas: mouse hover lights a spot (desktop only), click walks; touch: 1st tap = tooltip with "Walk there", 2nd tap walks; tap in the shadow leaves; floor tap clears. Esc / move keys leave.
- HelpSign.tsx: `.paper.manual.help-sheet` 340px right sheet; under 760px a bottom strip (46vh) and the HUD hides. Legend `.help-legend` numbered rows (hover/focus lights the spot), DOM tooltip `.help-tip` placed every frame from `tourRect`. The tour is set in a mount effect and cleared on unmount.
- Check script: Kelly 1's desk /home/agent/tools/tour-shot.mjs and tour-tap.mjs (phone: taps hotspot 3 twice at 337,192). Console: `window.musterTown.openPanel("help","bl_hzjw0z0zlz")`.

## Left over (minor)
- On the phone ". 1 resting." can wrap after the last name link. A tooltip near the top wall can cover a neighbouring hotspot.
- A guest who walks to a hotspot can take a long road (walked out and round to the door, ~25 s to the in-tray on the phone). This is the existing walk path, not the tour.
