---
id: "dc_s2qqo4ad9a"
type: "report"
state: "building"
title: "Style-guide skill dc_q736158pnn rewritten to main 76c6ad1 after PR 4: every anchor now points at panels/hiw.css, panels/PagedCard.tsx, home/home.css, home/preview.ts and server home.ts; preview smoothing recorded as the rule; no code changes"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_q736158pnn","dc_4g2vhywrxo"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Style guide rewritten to 76c6ad1 after PR 4; no code change. Acknowledged."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T19:06:44.308Z"
sessionId: "se_fkyc8f7wfl"
assignmentId: "as_0qji29w2qk"
costUsd: 3.3627645000000004
tokens: 27373
turns: 20
createdAt: "2026-10-26T19:06:25.967Z"
updatedAt: "2026-10-26T19:06:44.308Z"
---
## What I did

Pulled main (76c6ad1, which contains Craig's PR 4 6988a43), printed every file the skill cites with `cat -n`, and rewrote **muster-style-guide [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)** with `write` (id, type skill, state building). The pin (sp_cw05cs9icp, building, listed) still holds with the new description. No code was changed; nothing was pushed.

## Findings

What changed in the skill, section by section (all line numbers verified against main 76c6ad1):

1. **Paper CSS**: `styles.css:495-541` → `packages/web/src/panels/hiw.css` (palette on `.hiw, .paper` :5, card shell :6-7, hues :12-14, type :15-17, scene :18-19, foot/dots :28-31, `.hiw .btn, .paper .btn` :33-36, breakpoints 820h :37-40 and 420w :41-48). styles.css keeps only the HUD "?" (`.help-btn` :494-496).
2. **Card shell**: `panels/PagedCard.tsx` (Head/Scene/Arrow :11-18, `PagedCard` :23-59, `last: {primary, secondary?}` :27, keys :39-45, foot :50-55). `HowItWorks.tsx` is one page "Your first minute" (:15-27, key `musterTown.howItWorks.seen`); `home/HomeCard.tsx` is Funded → Legible → Projects with the tiles inside (:42-81, key `musterTown.home.seen`, "Open <first collective>" :79).
3. **Tiles**: `home/home.css` (.tiles :14, .tile :15-16, .tile-map :18, .tile-name :19, .tile-live :20-22, .tile.placeholder :23-24, .tile-soon :25, .tile-tag :26, 420px :33-38); same markup server-side in `server/src/home.ts` `tile` :46-57. Preview: `home/preview.ts` fetches `/api/town` every 20 s (:12), `drawOverview` (:47), pill "N working now" / "Resting now" (:31).
4. **Bend → rule**: the live preview is drawn below 1:1 at the zoom that fits the lots, with canvas smoothing like the minimap (preview.ts:40-43), not integer-scaled; integer scale stays the rule for sprite pictures. Written in section 6 and the Don'ts.
5. **`.goal` don't dropped**: home.ts has no `.goal`; tiles don't show the goal (said in section 6). Checklist item 1 now just says prefixed classes.
6. **Homepage plumbing**: new closing section "Where things live": second Vite entry `packages/web/home.html` → `src/home/` (vite.config.ts:22); the server renders `/` (`renderHome`, home.ts:63-103, served from app.ts:97) and copies the bundle's tags from `dist/home.html` per request (`homeBundleTags` :37-43); Workshop client stays at `/workshop/` (vite.config.ts:9).

Also updated: section 1 (`.paper` surface, home.css backdrop fixed), section 2 (sheet h1 and working-now dot use the green hue; dark hexes no longer hard-coded in home.ts), section 3 (tile name/tagline sizes, `.hud-town` kicker), section 4 (sheet frame 760px, tile hover lift), section 7 (`.paper .btn` for paper buttons outside the dialog), section 8 (copy anchors now home.ts:83-85, HomeCard.tsx:58), section 9 (hud.tsx TOUCH moved to :18), checklist 5 (mock mode: bare homepage bundle at `/workshop/home.html`; real `/` needs the server with a built dist). Each section is still under half a page.

Not in my assignment but in my inbox this session: Mitchell cut gr_cm3zha6mk6 (KR 1) at its checkpoint at 19:01Z; Root shipped manager `reassign`/`cancel` as 76c6ad1 (live after the next redeploy). Craig's queued KR 1 items and Tae's as_c7oiqdtlyz now sit on a cut grant; I'll cancel or re-lane them in my next team-lead session and ask Mitchell in the rollup whether the cut means done or pivot. Wiki pages "Style guide" and "Stranger path grant" rewritten accordingly.

## What I need from you

Nothing needed.
