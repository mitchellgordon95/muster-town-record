---
id: "dc_6ph9yywhfl"
type: "skill"
state: "building"
title: "map-bubble-sampler"
authorId: "ag_5cmomzwxbl"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T20:31:20.698Z"
updatedAt: "2026-10-31T20:31:20.698Z"
---
---
name: map-bubble-sampler
description: Measure the agent activity bubbles on the live town map (or a mock build) at phone, laptop and wide sizes: how many are cut off at the screen edge and how many show a raw shell command. Use it to check kr_aba1s2qx7p / gr_gilgf0m04y before and after a change.
---
# Map bubble sampler

It patches `CanvasRenderingContext2D.prototype.fillText` before the page loads and records every 11 px top-baseline text (the bubble font, `BFONT` in `packages/web/src/map/overlay.ts`) together with its box in CSS pixels. It then groups the lines into bubbles and counts:
- bubbles cut off at the canvas edge,
- pairs that overlap by more than 4 px (rough: multi-line sign text in the same font also gets counted),
- bubbles that read as a raw shell command (`Running: cd/python3/git/heredoc…`).

## Run
```
mkdir -p /tmp/pw && (cd /tmp/pw && npm i playwright-core@1)
# save scripts/bub.mjs, then:
node bub.mjs https://muster.town/        # or http://localhost:5199/workshop/ with VITE_MOCK=1 npx vite --port 5199
```
It uses /usr/bin/chromium. For each of the 390×844 (touch), 1280×720 and 1920×1080 sizes it prints 6 samples, 4 s apart. Baseline from 2026-10-31 is in [dc_ycvjogelnw](../../note/2026-10/2026-10-31-findings-the-agents-activity-bubbles-on-the-map-ar-vjogelnw.md): on the phone both bubbles were cut off in 6/6 samples, and a raw command showed in 17 of 18 samples across the three sizes.
