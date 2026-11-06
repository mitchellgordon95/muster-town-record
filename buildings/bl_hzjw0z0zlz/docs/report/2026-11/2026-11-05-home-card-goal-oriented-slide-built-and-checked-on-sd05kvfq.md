---
id: "dc_qesd05kvfq"
type: "report"
state: "building"
title: "Home card \"Goal-oriented\" slide built and checked on desktop and phone, not on main: stopped while Mitchell finalises the words"
authorId: "ag_agouimm1k3"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "redirect"
decisionNote: "Home card: replace the last slide (collective tiles) with the third pillar, FINAL copy from Mitchell (1:1 mt_45rqw4zl39, 19:06-19:12Z). Rebuild from the stopped work in dc_qesd05kvfq (same shape as the other two pages: heading, two arrows, scenes; keep the \"Open <collective>\" button). Exact words, no edits:\n- Heading: \"Goal-directed\" (NOT \"Goal-oriented\")\n- Sub: \"One goal tree: every agent works under a goal.\"\n- Arrow 1: \"Humans set goals and assign workers to subtrees\"\n- Arrow 2: \"Agents propose budgeted plans; humans fund them\"\nTwo arrows only, no third beat. Check the slide on desktop and phone (screenshots in the report), run the tests, open the PR and merge it green; do NOT call redeploy (CI deploys main). Report the commit sha and the screenshots."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-05T19:12:22.554Z"
sessionId: "se_x8khapv2i2"
assignmentId: "as_ap031w697c"
costUsd: 1.4305318
tokens: 71527
turns: 3
createdAt: "2026-11-05T19:10:07.342Z"
updatedAt: "2026-11-05T19:12:22.554Z"
---
## What I did
I replaced the homepage pitch card's third page (the collective tiles) with a "Goal-oriented" pillar, applied both wording changes Mitchell sent during the session, and screenshotted the slide at desktop and phone size. When Kelly said stop, I did not push to main. The work is committed as **c410581e** on branch `agent/kelly-1/home-card-replace-the-third-slide-collec` (pushed; no PR opened).

## Findings
- **What c410581e contains:**
  - `web/src/home/HomeCard.tsx`: a new page `GoalOriented` replaces `Projects`. The `Tile` component, `NOT_STARTED`, the `mountPreview` import and the react hooks are removed from the card. The tiles stay on the server-rendered page behind the card.
  - Copy on the new page: kicker "Muster Town is", h2 "Goal-oriented", sub "One goal tree: every agent works under a goal.", step 1 "Humans set goals and assign workers to subtrees" (Mitchell's 19:08Z wording), step 2 "Agents propose budgeted plans; humans fund them". Scenes are goals → tasks → work. The page uses the default blue hue. There are two steps only and no checkpoint beat: Mitchell dropped it, and the style guide allows at most two steps per page.
  - The last button is still "Open <first collective>". In mock mode there are no collectives, so no button shows there.
  - `web/src/panels/hiwScenes.ts`: a new scene kind `goals` (a goal box over two branch boxes, a small desk on each branch). No new assets.
  - `web/src/panels/hiw.css`: `.hiw-step` gets `text-wrap: balance`, which stops a long step from leaving one word alone on its second line.
  - The header comment, `server/src/home.ts` (its comment no longer points at HomeCard `Tile`), `docs/architecture.md` and `docs/log.md` are updated.
- **Overlay:** the in-town "How this works" overlay (HowItWorks.tsx) has its own pages, so this change doesn't touch it.
- **Checks:**
  - Mock-mode screenshots at 1400×900 and 390×844 show 0 console errors. The card fits the viewport at both sizes; step 1 is one line on desktop and two balanced lines on phone. Files on this desk: /tmp/p3-desk.png and /tmp/p3-phone.png. The script that pages to slide 3 is /home/agent/tools/shot-page3.mjs.
  - `npm run check --fast` exited 0. That run started before the final step-1 wording edit, which only changed copy.
- **Not done:** no push to main, no CI run, no live check. The style guide skill [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md), sections 5 and 7, still describes the tiles inside the card; Kelly owns it and I told them.
- **Next session:** `git merge` or cherry-pick c410581e onto main and change only the copy strings in `GoalOriented` (HomeCard.tsx, around line 44) plus the matching line in docs/log.md. Then run typecheck, re-shoot with shot-page3.mjs (start mock vite in `packages/web`, `VITE_MOCK=1 npx vite --port 5179`; stop it with `pkill -f "vite --port 517[9]"` in its own command, because it also kills the calling shell), push to main, `gh run list --branch main`, and live-check after the deploy.

## What I need from you
Send the final slide copy from Mitchell in the fresh assignment.
