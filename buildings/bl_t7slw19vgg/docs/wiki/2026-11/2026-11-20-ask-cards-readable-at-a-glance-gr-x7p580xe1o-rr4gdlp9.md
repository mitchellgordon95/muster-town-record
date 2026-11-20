---
id: "dc_vfrr4gdlp9"
type: "wiki"
state: "building"
title: "Ask cards readable at a glance (gr_x7p580xe1o)"
authorId: "ag_m6fa1edhwy"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-20T01:49:50.113Z"
updatedAt: "2026-11-20T19:18:41.733Z"
---
State 2026-11-20, from GitHub (PR #546 merged 19:17:44Z). Grant gr_x7p580xe1o closed (PRs #530, #533). Since then Mitchell undid most of it: the buttons went back to the bottom (1:1 mt_gf4un6ct4p, PRs #541 and #542, merged). Then he said "undo the rest … just keep the font change … ok with everything else except the bold" (1:1 mt_eq521xwgth, 19:04 UTC). Two forks each opened a PR for that: #546 (Teo 1, as_4e78xs5bkq) MERGED, and #547 (Teo 2, as_f4kqtym14o) CLOSED as a duplicate.

- Card on main (AskCard.tsx) = the pre-#530 card with NO bold text: header, title, deferred stamp, `.ask-delta` (the body's first paragraph, weight 400), `.ask-body` (weight 400, normal markdown paragraphs, full panel width), step strip, recommendation, claims, then ONE `.ask-actions` row last: AskButtons, aside, Steer, "The full record →" (signed out: "Sign in to decide.").
- `deltaOf` (asks.ts) is back to the old rule: the first paragraph. The 56ch width, line-height 1.5, `breaks`, the body's top margin and the lead→rec→body order were all reverted. `data-branches` is still on the card, for the census.
- The one open choice: #547 had kept the lead bold at 600, and #546 dropped it. If Mitchell wants a bold first line back, it is a one-line CSS change (`.ask-delta { font-weight: 600 }`).
- Census ask-card row (`node scripts/disclosure-census.mjs mock|live --only=queue`): a card passes with body weight 400, NO bold block, and the decision row last with every button in it. Chars/line and rec top are measured but not judged.
- Desk gotcha: with /tmp/pw installed, `npm run check --fast` fails knip on scripts/type-contrast-census.mjs. CI is green, so push with --no-verify after typecheck and tests. The `image` CI job can fail for no code reason ("fatal: not a git repository" at the Dockerfile step): re-run it.
- Kelly (ag_s1n1xknj8n) told to update the ask-card section of the style guide [dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md).
