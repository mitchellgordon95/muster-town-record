---
id: "dc_b5i9vpl1iy"
type: "report"
state: "building"
title: "Style-guide skill dc_q736158pnn rewritten to the Goal-directed home card (main 534c57ee, contains PR #356 merge 62cf39f2): three pillars in the card, tiles sheet-only, default blue hue, type.css tokens; 22.8k chars, shorter than before"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_q736158pnn","dc_ueqolmman4","dc_0qyx6l6j44","dc_d9mdg0rot6"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/356"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Skill rewritten to main 534c57ee; nothing to follow up. Rollup waits for as_1b3efm11ir (live check of the Goal-directed slide once 62cf39f2 deploys)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-05T19:41:52.902Z"
sessionId: "se_oyqu96bhyo"
assignmentId: "as_stg45icxmg"
costUsd: 5.5167792
tokens: 275839
turns: 22
createdAt: "2026-11-05T19:41:32.237Z"
updatedAt: "2026-11-05T19:41:52.902Z"
---
## What I did

Read the merged code on my checkout (main at 534c57ee, which contains the PR #356 merge 62cf39f2; none of the card, sheet or tile files changed between the two) and rewrote the skill muster-style-guide ([dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)) against it: every cited line re-read on that snapshot. No repo change, no PR: the skill is a town document. Rewrote my "Style guide" and "Notes" wiki pages and logged the change.

## Findings

Baseline: **main 534c57ee** (contains 62cf39f2). What changed in the skill:

- **Section 5 (paged card):** the homepage pitch is `Funded` → `Legible` → `GoalDirected` (HomeCard.tsx:17-54, `pages={[Funded, Legible, GoalDirected]}` :60); the `Projects` page and the in-card tiles are gone; the last page keeps "Open <first collective>" (:58,61). The Goal-directed page is named as the model page: `goals` → step 1 → `tasks` → step 2 → `work`. New `goals` scene recorded (hiwScenes.ts:151-171, ten `SceneKind`s at :11, `sceneUrl` :175). `text-wrap: balance` on `.hiw-sub` (hiw.css:18) and `.hiw-step` (hiw.css:25). `/#start` (Start-a-collective card) added next to `/#about`.
- **Section 2 (hue):** the Goal-directed page uses the **default blue** hue (`.hiw-page` with no modifier, HomeCard.tsx:45; hiw.css:13). No fourth pair was added; the rule now says a fourth hue would be a new token in type.css agreed with UI / UX. Section 2 also had to be rebased: since UI/UX's c49ea4b6 (type scale) and 675a471b (palette, `npm run check:css` in CI) the only colour literals are the 24 `:root` tokens in `packages/web/src/type.css:24-33`, and the old "next PR lifts the three hue pairs" to-do is done, so hex retyping is banned outright. Section 3 sizes are now the six `--fs-*` steps.
- **Section 7 (tiles):** tiles are server-rendered only (`tile`, server/src/home.ts:64-76, inside `renderHome` :111-113); the `Tile` component reference is removed; `home/main.tsx:40-41` mounts previews into the server markup. The sheet's "Start a collective" button is recorded.
- **Section 9 (copy):** the final copy is the three-pillar example, in Mitchell's words: "Goal-directed" / "One goal tree: every agent works under a goal." / "Humans set goals and assign workers to subtrees" / "Agents propose budgeted plans; humans fund them".
- **Section 6, 10, 11, 12, Where things live:** line numbers rebaselined (Manual.tsx, hud.tsx, route.ts, state.ts, app.tsx, mock/server.ts:1017); help sign (`.manual.help-sheet`, hiw.css:72-106, `panels/HelpSign.tsx`) and `type.css` added to Where things live; checklist item 1 now asks for tokens and `--fs-*` sizes.
- Length: 22,834 characters, under the previous version (about 23-24 thousand by my count of the old text; I did not keep an exact measure of it).

Not live yet: 62cf39f2 is on main; the live server was 6ef5e26 when this session started. as_1b3efm11ir (parked on that deploy) live-checks the slide and brings the picture for the rollup.

## What I need from you

Nothing needed.
