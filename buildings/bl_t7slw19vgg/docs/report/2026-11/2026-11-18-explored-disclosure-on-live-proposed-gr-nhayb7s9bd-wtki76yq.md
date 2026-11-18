---
id: "dc_5kwtki76yq"
type: "report"
state: "building"
title: "Explored disclosure on live; proposed gr_nhayb7s9bd: goal tree readable at first look (350k)"
authorId: "ag_fs5z20j9gc"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Disclosure holds (24 of 30 pass, the 6 fails are Mitchell's choice or document bodies). The money ask for gr_nhayb7s9bd is filed. The goal-detail count mismatch goes on the queue as a small exploration."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-18T00:16:58.436Z"
sessionId: "se_s7i2uww0tm"
assignmentId: "as_2yrbrzooye"
costUsd: 1.5431830000000004
tokens: 77159
turns: 38
createdAt: "2026-11-18T00:15:32.666Z"
updatedAt: "2026-11-18T00:16:58.436Z"
---
## What I did
- Re-ran the disclosure census on live cbfa71ee as a guest, at 1280×800 and 390×844.
- Measured the decision queue on the mock with a patched local copy of the census, because the census misses that sheet.
- Measured the goal tree's opening zoom and the size of its text.
- Wrote up the findings in [dc_1jzddih5xy](../../note/2026-11/2026-11-18-live-disclosure-re-census-2026-11-18-and-the-goal-zddih5xy.md), rewrote topic page [dc_qswk18hm5y](../../wiki/2026-11/2026-11-04-progressive-disclosure-gl-1ds3wl2n78-wk18hm5y.md), and filed proposal gr_nhayb7s9bd.

## Findings
- **Disclosure holds.** 24 of 30 live rows pass. The 6 fails are 3 cases, each seen at both sizes:
  - Onboarding Overview has 13 controls. This is Mitchell's own unfold request ([dc_7jyij2euj6](../../flag/2026-11/2026-11-17-also-nit-uncollapse-the-quick-action-buttons-on-th-yij2euj6.md)).
  - An agent's Memory tab has 371 words, which are wiki words.
  - A goal detail has 253 words, which are the key result's own text. It also shows a small mismatch: "KEY RESULTS (0)" above "3 done".
- **Census coverage dropped** from 70 rows to 30, because the live API now gives it 1 building and 1 agent. The decision queue sheet isn't measured at all. On the mock it passes: 8 controls, 164 words.
- **The goal tree opens unreadable.** The live tree has 23 goals over 4 levels. It opens on Fit at 21% on a laptop and 10% on a phone. Its 13 px titles (`--fs-md`) render at about 2.7 px and 1.3 px. The bottom row of 11 boxes is about 2,600 px wide, so no zoom level can fit it and stay readable. Folding the canvas is the fix.
- **Proposed gr_nhayb7s9bd, "Goal tree readable at first look"**: 350,000 tokens in 3 steps (M, M, S).
  1. Fold the canvas below level 2, open it at zoom ≥ 0.85, and add +N chips.
  2. Give phones a readable outline view.
  3. Add a readability column and a queue row to the census, then run it live.
  - It keeps the vertical canvas (mt_cyd2t5ioob) and Fit (PR #240).
  - The town's estimate: 3 similar grants spent 329k–368k.

## What I need from you
Fund, counter or reject gr_nhayb7s9bd in the Town Hall in-tray.
