---
id: "dc_6hza7i15p4"
type: "wiki"
state: "building"
title: "Rollup report view (calls first)"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-04T18:54:55.101Z"
updatedAt: "2026-11-04T19:36:42.440Z"
---
Mitchell asked in 1:1 mt_i50xwu4z2t (2026-11-04 18:25 UTC): "the reports themselves are still hard to read. maybe ask UI / UX to take a pass at the format + UI, while thinking about the progressive disclosure and overload goal". Assignments as_igsg6x1v1z → as_zi7zszpy17 → as_6zgscps94p (directed).

DONE 2026-11-04: PR #327 merged as b4e24d86, live since 4815e19 (19:33 UTC), verified on live at 1280×800 and 390×844 (checkpoint rollup [dc_n0ebhhhrsk](../../report/2026-11/2026-11-04-checkpoint-progressive-disclosure-grant-at-856-185-ebhhhrsk.md) as the sample): the "Your calls (2)" block is on the first screen at both sizes, 4 first-screen controls, the three folds closed ("Decided · 7 reports", "Key results and spend", "Provenance · 16 sources"), 3 cards. Crop mf_1s3cymt2qf; full shots on my desk /tmp/shots/rollup-live-{laptop,phone}.png. Rolled up in the rollup filed by as_6zgscps94p (says the manager prompt template changed town-wide).

How a rollup reads now: opened from the Town Hall in-tray (or any doc view), a "Your call" block on top (every Shipped item's real call plus the Needs lines; "Nothing to decide" when all are None), then the Shipped cards (a None call shows no gold line), then Decided, Key results and provenance folded in `<details>`. Code: packages/web/src/panels/RollupCards.tsx `RollupReport` (DocView uses it for tagged rollups; the in-tray row's expanded view uses rollupCardsOf), schema `rollupAsks` and `parseRollup().sections` (packages/schema/src/rollup.ts), CSS `.rollup-top` / `.rollup-fold`. Review deck (core review-deck.ts): a rollup's Needs lines ride on its first slide, or make its one slide (`rollup:<id>:needs`) when no item asks a call. Manager prompt template (core prompts.ts MANAGER_INTRAY_RULES) says how a rollup is read and caps "What it is" at ROLLUP_MAX_WHAT_WORDS = 80 words (filed with a warning over it): this touches every building's manager prompt. Mock rollup dc_moss_rollup is in the labelled format.

Measured on the mock at 1280×800 (two items, one real call): before 1.9 screens with the call last; after 1.4 screens, 2 controls, 175 first-screen words, the call first (mf_tszb2vjzkb after, mf_cjvdpp0f77 before).

Screenshot script: /tmp/shots/rollup-shot.mjs on my desk (rebuild if /tmp is gone: playwright-core@1 in /tmp/pw, chromium at /usr/bin/chromium; `node rollup-shot.mjs <docId>` prints first-screen controls/words/folds at both sizes and writes the shots). An agent token in localStorage is refused by the web client ("browsing as a guest"), so live shots are guest views; the renderer is the same.

Coordination: Pix merged #317 (grouped digest card) as d156a72; Pix's follow-up (tell ms_uo54lm4ltl) switches secretary.ts digestDecisions to `rollupAsks(parseRollup(body))` so the card and the report quote the same lines.

Not done / ideas: the in-tray one-line list (intrayList.tsx) shows only the title and a "rollup" pill; it could show the first call. The deck's rollup slide still renders the full card. A long title (my checkpoint's is 30 words) plus the intro paragraph push the calls block to y≈330 at laptop; shorter rollup titles help.
