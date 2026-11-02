---
id: "dc_71toiuzway"
type: "report"
state: "building"
title: "Grant step 4 pushed: GET /api/review-deck and \"Review as deck\" in the Town Hall in-tray (e74ae79 on main, redeploy queued)"
authorId: "ag_78l83jtucz"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Step 4 on main at e74ae79, redeploy done. Its proposal (live check parked on e74ae79) already exists as as_pnfwdnaw8k, which now runs: step through the deck, decide one item from a slide to see deckSlide in the event log, take the rollup-30 screenshot. Migration 053 was authorised by the assignment. Gaps noted for step 6: met/missed from a slide carries no deckSlide, countered proposals and access requests have no slide, no per-slide URL hash."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T04:12:05.343Z"
sessionId: "se_6kzhkxx2rt"
assignmentId: "as_oc8fmtg3wa"
costUsd: 5.062846099999997
tokens: 253142
turns: 95
createdAt: "2026-10-29T04:10:40.575Z"
updatedAt: "2026-10-29T04:12:05.343Z"
---
## What I did
I built step 4 of gr_jh0lu0w6yj (design [dc_y7a8g257of](../../article/2026-10/2026-10-28-design-the-review-deck-in-tray-review-as-a-present-a8g257of.md) §2) from scratch and committed it straight to main as **e74ae79**, rebased on 0f1027b. I called `redeploy` once. Nobody has checked it on the live site yet: e74ae79 should be live after the redeploy. I updated the topic page [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md).

## Findings
**What is on main (e74ae79):**
- **`GET /api/review-deck`** is built in `packages/core/src/review-deck.ts` (`reviewDeck(world)`). It is assembled from `townHallIntray()` plus key results and costs zero tokens. The types (`ReviewDeck`, `ReviewSlide extends DeckSlide`, `isNoCall`) are in `schema/src/deck.ts`.
- **Slide 1** shows:
  - the Bank balance;
  - subscription spend today against the learned cap;
  - exploration spend against its allowance, and directed spend (from `laneBudgets`);
  - one row per building, with its stoplight and each key result as a stoplight emoji;
  - "N decisions below, oldest waiting X h";
  - one line for flags still pending after 2 h.
- **Then one slide per decision**, in this order:
  1. Held checkpoints.
  2. Blocked buildings.
  3. Items that work is parked on, most waiters first. Waiters are pending assignments with `waitFor {decision}`, which covers parked continuations too.
  4. Proposals, oldest first.
  5. Rollup items whose Your call is not None (one slide each, via `parseRollup`), plus other reports: old-format rollups, visitor and checkpoint reports, shown as their markdown.
  6. Grants closed as done.
  7. Last, one **For the record** slide for rollups whose every call is None, with **Approve all**.
- **What each slide shows:** the wait and waiter count at the top, then What it is / What you'd see / picture (or "no picture") / Your call. A proposal's slide is built from its fields: objective → what it is, `whatYoudSee` or the testing plan's howToCheck → what you'd see, ask + stop condition → your call, and the picture is its own or the first media in its findings docs.
- **One history line per slide** when one applies:
  - for a grant: its last human entry;
  - for a rollup: the same building's previous rollup decision and its note;
  - otherwise: the decision of a human meeting named in its provenance (a `mt_` id or a meeting-notes doc).
- **Web:** a **▶ Review as deck** button in the Town Hall in-tray header opens `panels/ReviewDeck.tsx`. It has ← → / space / Home / End, the counter and dots, `f` for fullscreen, and Esc to go back to the list.
  - The decision buttons under each slide are the existing ones: GrantRow, and the report's Talk to plus the reply/archive box.
  - Deciding reloads the deck and lands on the next item's slide.
- **`payload.deckSlide`** is recorded on grant decide events (fund, counter, reject, continue, adjust, cut) and on reply/archive `doc.decision` events.
- **`propose_grant`** now takes optional `picture` (mf_…) and `whatYoudSee`. They are stored on the grant through **migration 053**, which adds two columns to `grants`. That is a schema migration; the assignment authorised it.
- `docs/manual.md` got one sentence and stays under the cap (1,897 words by the test's count); the manual test passes.

**Tests, all green:**
- core: all 74 files pass, including the new `review-deck.test.ts` (5 tests: ordering, waiter counts, For-the-record collapse, history lines, deckSlide, picture). On this desk the suite takes longer than 10 minutes, so I ran it in batches with `--testTimeout=30000`; at the default 5 s, the wakes tests time out.
- server: 25 files, 131 tests, including the new `review-deck.test.ts`.
- web: 30 files, 116 tests, including the new `reviewDeck.test.tsx` (3 tests).
- typecheck is clean in every package.

**What is not on main:**
- Marking a key result met or missed from a slide does not carry `deckSlide`.
- Countered proposals and access requests get no slide; access requests are counted on slide 1.
- The deck view has no URL hash per slide.
- Step 5 (Presentation mode, the `Meeting.deck` migration) has not been started.
- Next step: a live check parked on {deploy: e74ae79}. Open the Town Hall in-tray, press Review as deck, step through the slides, and decide one item from a slide to see `deckSlide` in the event log.

## What I need from you
Nothing needed.
