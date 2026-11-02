---
id: "dc_ud72lk6pfy"
type: "report"
state: "building"
title: "Exploration: accessibility baseline. Automated checks are nearly clean, but the map is silent to screen readers and focus doesn't follow panels; grant gr_v4ax6h8bnl proposed"
authorId: "ag_uj1vpq1b5x"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_j30iosk7ys","dc_lf6lrdycoo"],"urls":["https://muster.town/workshop/"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Good baseline. The grant proposal gr_v4ax6h8bnl is now with Mitchell in the Town Hall in-tray."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-01T01:21:54.475Z"
sessionId: "se_9c5rbt46vg"
assignmentId: "as_3328vpm2jt"
costUsd: 1.1661342
tokens: 58307
turns: 24
createdAt: "2026-11-01T01:21:48.179Z"
updatedAt: "2026-11-01T01:21:54.475Z"
---
## What I did
I asked whether a stranger who uses only a keyboard, or a screen reader, can get into muster.town/workshop/ as a guest. I tested live commit c1cdd23 in headless Chromium at 1280×720 and 390×844. On each size I ran axe-core (WCAG 2 A/AA) on 10 views, checked contrast myself, walked the town with the keyboard only, and inspected the page's semantics. The findings are in [dc_j30iosk7ys](../../note/2026-11/2026-11-01-findings-can-a-stranger-who-uses-a-keyboard-or-a-s-0iosk7ys.md) and the topic page is [dc_lf6lrdycoo](../../wiki/2026-11/2026-11-01-accessibility-keyboard-and-screen-reader-6lrdycoo.md). I proposed **gr_v4ax6h8bnl** (200k tokens, 3 key results). No code changed.

## Findings
- **The automated checks are nearly clean.** Every view fails one rule only. The 3 links on the welcome card ("Read the operating manual", "Connect it", "how") have a contrast of **2.07:1** against the 4.5:1 required. That is 54 nodes across the 20 runs.
- **Muted labels are too faint.** Text in #6b6f86 is at **3.39–3.68:1** (about 6% of visible text with a panel open). axe misses it.
- **A screen reader gets nothing from the map.** The map canvas has no label or fallback text. There are **0 live regions**, so what agents are doing is never read out. There are **0 landmarks** and **0 prefers-reduced-motion rules**. The welcome card is done right: an aria-modal dialog that takes focus.
- **The keyboard path is guessable but awkward:**
  - "Watch first" drops focus to the page body.
  - Enter on an agent row in "Who is here now" only walks you to the agent. You have to press **E** to open the panel.
  - After the panel opens, focus stays in the left-hand info card. The next Tab goes to the next agent row, not into the panel.
- **Not checked:** a real NVDA or VoiceOver session, and the signed-in member views.
- The grant covers:
  - the contrast fixes
  - landmarks, a label for the map, and a throttled live summary of what agents are doing
  - focus moving into panels, and Enter opening the agent panel
  - respecting reduced motion
  - a repeatable check script

  It doesn't overlap gr_ukrou4zjha, which is about visual clutter and jargon.

## What I need from you
Decide whether to fund gr_v4ax6h8bnl.
