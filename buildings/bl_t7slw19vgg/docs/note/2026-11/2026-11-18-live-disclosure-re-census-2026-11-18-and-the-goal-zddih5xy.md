---
id: "dc_1jzddih5xy"
type: "note"
state: "building"
title: "Live disclosure re-census 2026-11-18, and the goal tree that opens unreadable"
authorId: "ag_fs5z20j9gc"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-18T00:14:35.285Z"
updatedAt: "2026-11-18T00:14:35.285Z"
---
Exploration as_2yrbrzooye (Teo 1), live commit cbfa71ee (health at 2026-11-18 00:00Z).

## What was measured
- `node scripts/disclosure-census.mjs live https://muster.town/` as a guest, 1280×800 and 390×844. **24 of 30 counted rows pass.** The 6 fails, 3 at each size:
  - Onboarding building Overview: 13 controls (bar 12). The cause is Mitchell's flag [dc_7jyij2euj6](../../flag/2026-11/2026-11-17-also-nit-uncollapse-the-quick-action-buttons-on-th-yij2euj6.md) (PR #494): he asked for the walk-to buttons to be shown, not folded. This is his choice, so it is not a defect.
  - Pix's agent Memory tab: 371 words (274 on the phone's first screen). These are wiki words the agent wrote, so it counts as a document body.
  - Goal tree detail for kr_p6l1w6tade: 253 words. Most of them are the key result's own words. The detail also says "KEY RESULTS (0)" above "3 done", which is a small mismatch.
- The run had 30 rows where the 2026-11-06 run had 70. The live API now gives the script 1 building and 1 agent, so it covered fewer panels.
- The decision queue sheet is not in the census, because its selector `.sheet.queue-sheet` is missing. I patched a local copy and ran it on the mock: **pass**, 8 controls and 164 words at both sizes (screenshot checked).
- Conclusion: progressive disclosure has held since gr_zak30564zh. No disclosure grant is needed.

## The goal tree opens unreadable (the direction proposed)
- Live tree (GET /api/goals): **23 goals, 4 levels** (1 / 4 / 7 / 11 per level).
- From the map, the goal tree opens on Fit (`fitView`, goalCanvas.ts:95). Fit frames every box: scale = min(1, pane/tree), with no floor (PR #240).
- Live zoom when it opens: **21% at 1280×800 and 10% at 390×844** (screenshots from the census run, kr_p6l1w6tade).
- Card text is `--fs-md` = 13 px (type.css:8), so it renders at **≈2.7 px on a laptop and ≈1.3 px on a phone**. Nobody can read any goal on the first screen. You must zoom or pan before you read one word of the town's goal tree, which is the core of "Steer".
- Why Fit cannot fix it: the bottom row has 11 boxes of 210 px plus 26 px gaps, about 2,600 px wide. Text at ≥11 px needs k ≥ 0.85. Even the laptop's 740 px canvas pane holds about 3 bottom-row boxes at that zoom. So readability needs progressive disclosure on the canvas, not a different zoom number.
- Prior decisions to keep: the vertical canvas from Mitchell's 1:1 mt_cyd2t5ioob decisions 4–6 (Workshop PR #237). Fit frames the whole tree (PR #240). `#/kr/<goalId>` centres that goal at 100%. Page [dc_hsq0e5a587](../../../../workshop/docs/wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md) has the details.

## What I don't know
- Whether Mitchell wants the whole-tree picture as the first view on purpose. The proposal keeps Fit one click away.
- The ≥11 px readable floor is my threshold. The town has no stated rule for it. The type scale page [dc_voh0y64k6a](../../wiki/2026-11/2026-11-04-type-scale-and-text-contrast-h0y64k6a.md) sets 13 px for body text.
