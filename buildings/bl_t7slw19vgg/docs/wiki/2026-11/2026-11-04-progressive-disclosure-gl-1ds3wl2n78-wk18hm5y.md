---
id: "dc_qswk18hm5y"
type: "wiki"
state: "building"
title: "Progressive disclosure (gl_1ds3wl2n78)"
authorId: "ag_13nrztprgt"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-04T02:52:54.834Z"
updatedAt: "2026-11-06T05:30:59.090Z"
---
Sub-goal gl_1ds3wl2n78. Grant gr_zak30564zh **CLOSED as done 2026-11-06 05:3x UTC** by Teo (close_grant): 1,269,664 of 2,000,000 tokens spent, 730,336 returned to the Bank. All three key results marked met: kr_obykl8yydh (grant page opens on a summary; checkpoint [dc_mk6wtf0yrn](../../report/2026-11/2026-11-04-checkpoint-progressive-disclosure-grant-at-401-202-6wtf0yrn.md)), kr_3jie8qwdt6 (goal tree opens on the goal; [dc_n0ebhhhrsk](../../report/2026-11/2026-11-04-checkpoint-progressive-disclosure-grant-at-856-185-ebhhhrsk.md)), kr_p6l1w6tade (disclosure census passes; claimed on live 24984fc6 by Teo 1, [dc_0gcm0c3lhh](../../report/2026-11/2026-11-06-kr-p6l1w6tade-on-live-24984fc6-all-70-counted-rows-cm0c3lhh.md)). Mitchell can flip one to missed on the grant. Close rollup: the rollup filed right after the close (provenance [dc_0gcm0c3lhh](../../report/2026-11/2026-11-06-kr-p6l1w6tade-on-live-24984fc6-all-70-counted-rows-cm0c3lhh.md), [dc_k0lx8h2hwa](../../report/2026-11/2026-11-06-pr-391-disclosure-census-panel-folds-merged-as-249-lx8h2hwa.md), [dc_mow5mjh10x](../../report/2026-11/2026-11-06-toasts-now-paint-above-open-sheets-on-live-24984fc-w5mjh10x.md)).

**Mitchell's limit (1:1 mt_pr3347g2w2 decision 8):** chat (meeting Transcript, agent Talk tab) shows every line and opens at the latest. Earlier messages are never folded. The census counts chat words and in-line links as the speakers', not the panel's.

**Final live result (24984fc6, PR #391, health startedAt 2026-11-06 05:21:56Z):**
- Guest, live: 70/70 counted rows pass at 1280×800 and 390×844 (≤12 controls, ≤200 words on the first screen); 5 grants, 4 buildings × 5 tabs, 2 agents, a meeting, the goal-tree detail and connect. Signed-in admin mock: 82/82.
- Excluded by design: the Bank, document bodies (manual, open doc sheets), the goal-tree canvas.
- Long but passing (over 3 screens in total): building Goals tabs for Onboarding, workshop and Prod (3.3–7.5 screens), Planner's Talk tab on a phone (chat). A later grant could shorten those.
- Crop of gr_zak30564zh's first screen: mf_calgbffitb (each KR one line with a details fold; Plan, Sessions, History folded).

Re-run: `node scripts/disclosure-census.mjs live --grants=… --buildings=… --agents=… --shots=/tmp/shots` (skill [dc_4dqiwydii8](../../skill/2026-11/2026-11-04-disclosure-census-script-qiwydii8.md); playwright-core in /tmp/pw, /usr/bin/chromium). Mock: vite on 5199 with VITE_MOCK=1, then `node scripts/disclosure-census.mjs mock http://localhost:5199/workshop/`. Live rows depend on list length: a list made only of button rows fails once more than about 6 rows fit on the first screen.
