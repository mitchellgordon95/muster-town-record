---
id: "dc_tmvfyiako2"
type: "report"
state: "building"
title: "Help sign tour built (PR #314): lit building, shadowed town, numbered hotspots; parked on CI"
authorId: "ag_k03dhtim0x"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked continuation (as_8mx54p514f) is already merging PR #314 and redeploying; nothing more to queue. Folded into the next rollup once it's live."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-04T18:27:50.312Z"
sessionId: "se_2awyedn9ow"
assignmentId: "as_x1rofjqu1c"
costUsd: 2.342330799999999
tokens: 117117
turns: 45
createdAt: "2026-11-04T18:16:30.917Z"
updatedAt: "2026-11-04T18:27:50.312Z"
---
## What I did
Built Mitchell's flag [dc_qppl7741ci](../../flag/2026-11/2026-11-04-i-like-the-content-of-the-little-question-mark-sig-pl7741ci.md): the "?" help sign now gives a tour of the building on the map. It's in PR #314 (https://github.com/mitchellgordon95/muster-town/pull/314): new map/tour.ts, plus changes to renderer.ts, MapCanvas.tsx, HelpSign.tsx and hiw.css, and a new test/tour.test.ts. CI was still pending when I parked.

## Findings
- **The tour:** when the sign opens, the camera frames the building's lot in the space the sheet leaves free. The rest of the town gets a dark shadow, and a paper glow outlines the lot. Each thing the card lists (board, cabinet, in-tray, schedule board, meeting table, desks) is a numbered dashed hotspot on the map.
- **Desktop:** hovering a hotspot shows a paper tooltip with the card's own line (no new copy) and lights the matching legend row. Hovering or Tab-focusing a row lights its hotspot. A click walks there and opens the thing.
- **Touch:** the first tap shows the tooltip with a "Walk there" button. A second tap, or the button, walks there.
- **Leaving:** Esc, the ×, a click or tap in the shadow, walking keys, or walking to a thing all end the tour. The shadow only exists while the card is open, so the map can't stay dimmed after the card is gone.
- **The card:** it is now a 340px paper side sheet; under 760px it is a bottom strip, and the HUD hides while it is open so the building has room. The content and the guest / pending / member / reviewer logic are unchanged. "What's here" is now the numbered legend for the hotspots.
- **Checked in mock mode** at 1400×900 with a mouse and 390×844 with touch as a guest, and I looked at the screenshots. Every interaction behaved as described above, and there were 0 console errors.
  - One bug found and fixed while checking: on touch, the first tap walked straight away instead of showing the tooltip.
- **Tests:** typecheck is clean and all 311 web tests pass, including 3 new ones for the hotspot geometry.
- **Small leftovers:** a tooltip near the top wall can cover a neighbouring hotspot. The tour's plan is on topic page [dc_axuboivkud](../../wiki/2026-11/2026-11-02-help-signs-in-every-building-flag-dc-8dwch9z5pi-uboivkud.md).

## What I need from you
Nothing needed. When CI finishes I'll merge PR #314, redeploy, and check it live on muster.town.
