---
id: "dc_vsh97095gs"
type: "report"
state: "building"
title: "Exploration: map bubbles cut off on phones and showing raw shell commands; grant proposed (gr_gilgf0m04y)"
authorId: "ag_5cmomzwxbl"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_ycvjogelnw","dc_6ph9yywhfl","dc_fsi2uzw9ty"],"urls":["https://muster.town/"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Solid measurement (18 live samples, causes cited at overlay.ts:113 and describe.ts:74). gr_gilgf0m04y already waits for Mitchell; nothing runs until it's funded."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-31T20:31:39.360Z"
sessionId: "se_5tz8y918qg"
assignmentId: "as_zc58yonztj"
costUsd: 1.4401028
tokens: 72005
turns: 42
createdAt: "2026-10-31T20:31:35.213Z"
updatedAt: "2026-10-31T20:31:39.360Z"
---
## What I did
- Opened all 16 panel kinds and their tabs (36 views) in mock mode at 390×844 and at 1280×720, checking for overflow, clipping and small text.
- Opened live muster.town as a guest at 390×844, 1280×720 and 1920×1080 and recorded the agents' activity bubbles from the canvas: 6 samples per size, 18 in all.
- Wrote findings [dc_ycvjogelnw](../../note/2026-10/2026-10-31-findings-the-agents-activity-bubbles-on-the-map-ar-vjogelnw.md), key result kr_aba1s2qx7p, proposal gr_gilgf0m04y (200k tokens) and the skill [dc_6ph9yywhfl](../../skill/2026-10/2026-10-31-map-bubble-sampler-h9yywhfl.md), which re-runs the measurement. Updated topic page [dc_fsi2uzw9ty](../../wiki/2026-10/2026-10-29-ui-ux-goal-and-key-results-i2uzw9ty.md).

## Findings
- **The panels are fine.** In all 36 views, nothing overflows the screen and nothing needs a horizontal scrollbar. The only weak spot is the Goal tree: 60 elements are under 11 px. I dropped the draft key result "panels render cleanly".
- **The map bubbles are the problem.** On a phone, both visible bubbles were cut off at the screen edge in 6/6 samples. At 1280×720, 1–2 bubbles were cut off in 6/6 samples. A bubble showed a raw shell command in 17 of 18 samples, for example `Running: cd /tmp; python3 - <<'EOF' import…` and `Running: curl -s -X POST "$AGENT_TOWN_UR…`.
- **Causes:** `drawBubble` (`packages/web/src/map/overlay.ts:113`) never clamps a bubble to the canvas and never moves one bubble off another; `drawTip` in the same file already clamps. `describeBuiltin` (`packages/runtime/src/describe.ts:74`) echoes the command whenever a Bash call has no description.
- **The proposal (gr_gilgf0m04y):** keep bubbles on screen and off the HUD, push overlapping bubbles apart, and describe undescribed commands in plain words, then check with a mock-mode playwright test and the live sampler. It stops when the live sampler shows 0 cut off and 0 raw at 390 and 1280 wide, or at 200k tokens.

## What I need from you
Decide whether to fund gr_gilgf0m04y.
