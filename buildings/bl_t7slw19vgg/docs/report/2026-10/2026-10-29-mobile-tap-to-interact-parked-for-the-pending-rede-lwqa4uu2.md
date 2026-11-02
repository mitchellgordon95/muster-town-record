---
id: "dc_cnlwqa4uu2"
type: "report"
state: "building"
title: "Mobile tap-to-interact: parked for the pending redeploy before coding"
authorId: "ag_xq9eg32fas"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked cleanly. The continuation is already queued as as_g8qy4lvxen (waits for the next deploy). Rebase on Teo 1's tap-to-walk work (as_bujlq7v4wj) once it merges."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-29T23:25:40.445Z"
sessionId: "se_x8uu5ri9uj"
assignmentId: "as_b3pnrqceg8"
costUsd: 0.2355826
tokens: 11779
turns: 6
createdAt: "2026-10-29T23:25:35.148Z"
updatedAt: "2026-10-29T23:25:40.445Z"
---
## What I did
Just started as_b3pnrqceg8 (from Mitchell's 1:1 mt_jzoyqe2lea). Ran `look` and a first pass over the code. Then a Redeploy interrupt said the server restart was waiting for my session to end. I hadn't changed any code, so I'm parking the work instead of holding up the deploy. Nothing is committed or pushed, and no commit of mine needs to go live.

## Findings
Plan for the next session:
- **Which kinds count.** The live place kinds are bank, bank-map, door, mod-station, planning, intray, schedule, bench, library, town-map, outbox, meeting-room, plaza, desk, board and cabinet.
- **Where interaction happens now.** Proximity interaction lives in `packages/web/src/map/renderer.ts` `updateTarget()` (around line 384). bank-map and town-map are special-cased there. Every other kind goes through `PLACE_PANEL[p.kind]`, which gives a verb and a panel, and is reached only by walking within `INTERACT_PX` and pressing the key or Tab.
- **Where to add the click.** Clicks are handled in `map/MapCanvas.tsx` `onClick` (around line 142). The next step is to hit-test places there:
  - Tap target: about 1.5 tiles around `p.pos`.
  - Agents are hit-tested first.
  - On a hit, walk to the place if the interaction needs you nearby, then open the same panel or action that `PLACE_PANEL` / the special cases give.
  - A tap on empty ground keeps the sibling "tap to walk" behaviour. Check whether that PR has merged and rebase on it.
- **Before and after.** The PR description gets the before/after list of kinds. Then run typecheck and tests, merge if green, and redeploy.

## What I need from you
Nothing needed.
