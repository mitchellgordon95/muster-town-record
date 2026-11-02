---
id: "dc_004hyy29z6"
type: "wiki"
state: "building"
title: "Town layout: doors on any side, the planned \"fountain\" town"
authorId: "ag_9otsjzyg2u"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-10-31T21:46:41.968Z"
updatedAt: "2026-10-31T22:44:54.839Z"
---
Mitchell asked for this in 1:1 mt_3ldf9p5av1 (2026-10-31): doors on any side, and make the "fountain" shape a planned town that feels like a town. Chain as_6gd7y6u4yz → … → as_vruux1eo99 ([dc_8aitzef4qj](../../report/2026-10/2026-10-31-fountain-town-and-doors-on-any-side-verified-live-itzef4qj.md)) → polish as_1yxoufc9ex → as_55s7k3cncd → live check as_ggz7wa8fmf. **Done.**

**Now true (live f729e03, checked 2026-10-31 22:43 UTC):**
- PR #205 (98a9fac): fountain layout and doors on any side. Live map is on **fountain**. core `world/road.ts` (`Side`, `doorOf`, `doorstepOf`, `insideOf`), core `world/square.ts` (square with fountain, Town Hall north, Bank south, one district per first-level goal; 8×7 lawn right of the Bank kept for the marquee).
- PR #220 (8c8389c): the Bank marquee shrinks (never below half size) to fit the clear tiles before the next lot, minus one tile (web `map/renderer.ts`, `overlay.ts drawBankSign(maxW)`). Live at 1280×720: zoom 3 and zoom 2 both end about 1 tile short of the UI/UX wall. On phone (≤760px) the town planning `.layout-bar` sits at the bottom, clear of the HUD card (styles.css; tap hint hidden while planning is open, app.tsx).

**Not this work:** on phone a guest lands inside a building and sees no street (kr_c3c7651d18, gr_ukrou4zjha). Town planning on phone cuts off the west districts. Noted, not fixed.

**Screenshots (desk cache, ~/shots):** `MUSTER_TOWN_URL=https://muster.town npx vite --port 5173 --force` in packages/web, then `node ~/shots/fix.mjs http://localhost:5173/workshop/ TAG` (both sizes plus town planning) and `node ~/shots/bank.mjs TAG` (camera on the Bank at zooms 3/2/4). Production muster.town can't move the camera to the Bank from a script (bundled modules), so Bank shots use the dev client at the live commit against live data.
