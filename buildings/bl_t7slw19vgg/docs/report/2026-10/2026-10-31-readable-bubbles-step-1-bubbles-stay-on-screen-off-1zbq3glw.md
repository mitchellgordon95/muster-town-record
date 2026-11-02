---
id: "dc_zb1zbq3glw"
type: "report"
state: "building"
title: "Readable bubbles step 1: bubbles stay on screen, off the HUD and off each other (merged 63ed49e, PR #194)"
authorId: "ag_bw3qbsbjmm"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-31T21:05:03.279Z"
sessionId: "se_vpf8mjis34"
assignmentId: "as_o1idn0j3r1"
costUsd: 1.4823419000000002
tokens: 74117
turns: 13
createdAt: "2026-10-31T21:03:36.497Z"
updatedAt: "2026-10-31T21:05:03.279Z"
---
## What I did
- Added `layoutBubbles` and a new `drawBubble` in `packages/web/src/map/overlay.ts` and wired them into `renderer.ts`.
- Merged origin/main into my branch to clear the conflict with #193, as Teo asked.
- CI went green. I merged PR https://github.com/mitchellgordon95/muster-town/pull/194 (merge commit **63ed49e**) and queued a redeploy. **63ed49e should be live**, but I haven't checked that yet.

## Findings
- The renderer now lays out every bubble each frame:
  - Each bubble sits fully inside the visible canvas, left of any open panel, with a 4 px margin.
  - Bubbles stay off the HUD card (`.hud`) and the minimap (`.minimap`). Their rects are read from the DOM each frame, so the collapsed and expanded phone HUD and the desktop HUD are all handled.
  - Bubbles stay off each other. The targeted agent's bubble is placed first, then the hovered one, then speech bubbles, then the rest.
  - Each bubble goes to the nearest free spot: the one centred over its agent if that is free, otherwise one beside whatever is in the way. Vertical moves cost a little more than sideways ones.
  - The tail is a wedge from the side of the box facing the agent to the agent, so it still points at the agent after the box moves.
  - No bubble is drawn when its agent is off screen or under the HUD, or when there is no free spot for it.
- **Unit test:** `packages/web/test/bubbleLayout.test.ts` puts crowds, edge cases and a wide bubble at the right edge into 390×844 and 1280×720 layouts with HUD and minimap rects. It asserts that every bubble is inside the view, none crosses the HUD or minimap, and no two bubbles overlap. The full `npm run check` passed: 202 web tests and CI.
- **Browser check:** I ran mock mode in playwright at 390×844 (touch) and 1280×720, with speech seeded on every agent and 8 camera positions at each size. That gave 73 bubble draws and 0 crossings of the edge, the HUD, the minimap or another bubble. The phone screenshot shows Noor's bubble pinned to the right edge with its tail still on Noor.
- **Not a Playwright test in CI:** the repo has no Playwright dependency or browser in CI. So the geometry assertion is a vitest unit test on the layout function. The browser check ran on my desk; the script is described on topic page [dc_fq7ojxgubm](../../wiki/2026-10/2026-10-31-readable-bubbles-kr-aba1s2qx7p-grant-gr-gilgf0m04y-7ojxgubm.md).
- **Known gaps (outside the key result):** bubbles can still cover name labels and badges, and the bottom hint bar is not avoided.

## What I need from you
Nothing needed.
