---
id: "dc_mzl50a5xsh"
type: "report"
state: "building"
title: "Avatar size by model tier pushed to main (f5da288), redeploy queued"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "as a followup, can i get model selection in the resident view? probably underneath the permissions settings?"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:03:21.706Z"
sessionId: "se_tmrg9r35hg"
assignmentId: "as_bq3amzhsef"
costUsd: 0.5351678999999999
tokens: 28946
turns: 24
createdAt: "2026-10-21T04:00:37.195Z"
updatedAt: "2026-10-21T04:03:21.706Z"
---
## What I did
- Added `packages/web/src/map/avatarSize.ts`, which works out an avatar's tier from its model ID, and connected it to the map renderer.
- Added unit tests. Checked the result in the mock UI with screenshots of agents at desks and in a meeting room.
- Pushed to main as **f5da288**. Redeploy is queued, so f5da288 should be live once this session ends.

## Findings
- **Tiers.** The tier comes from the agent's own `model`. If that is empty it uses the home building's `model`. Anything else, including no model or an unknown one, gets standard size.
  - **XL:** model ID contains fable or astra. Drawn at 15×20 px, which is 1.25x.
  - **Standard:** opus, sol, or anything else. 12×16 px, which is 1x.
  - **Small:** sonnet, luna or haiku. 10×14 px, about 0.85x (0.83 wide, 0.875 tall).
  - I used whole-pixel sizes so the pixel art stays sharp.
- **What scales with the body:** the shadow, the click hitbox, the "⟳ redeploy" pill and where speech bubbles attach. Bodies stay anchored at the feet, so name labels stay where they were.
- **Overlap at desks:** none. Every size is narrower than a 16 px tile, and desks are 4 tiles apart. Screenshot: ~/shots/avatar-desks.png.
- **Overlap in meeting rooms:** I packed six agents onto neighbouring tiles, two rows of three, which is tighter than real seating. Side by side, no bodies overlap. In the row behind, the top ~4 px of an XL head can show above the front row; the map draws back to front, so it looks like normal depth. Screenshot: ~/shots/avatar-meeting.png.
- **Name labels** still overlap when agents stand on neighbouring tiles. That happened before this change too, because labels are a fixed size.
- **Checks:** `npm run typecheck` is clean and web vitest passes 33/33, including the new `avatarSize.test.ts`. I haven't checked it on the live server yet; I'll do that next session.

## What I need from you
Nothing needed.

## Reply from Mitchell (2026-10-21 00:03)

as a followup, can i get model selection in the resident view? probably underneath the permissions settings?

