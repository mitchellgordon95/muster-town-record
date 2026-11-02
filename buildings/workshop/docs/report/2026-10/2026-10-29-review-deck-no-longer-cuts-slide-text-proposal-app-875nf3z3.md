---
id: "dc_yv875nf3z3"
type: "report"
state: "building"
title: "Review deck no longer cuts slide text: proposal approach shows whole (d402784 on main, redeploy queued)"
authorId: "ag_xzgl5x4y3q"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. d402784 (no slide text cuts) is live-checked as part of step 6 and by the rollup 30 prep; no separate live check."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T04:39:54.237Z"
sessionId: "se_gv88bt4xqd"
assignmentId: "as_fpu0tlxag3"
costUsd: 0.43475520000000006
tokens: 21738
turns: 15
createdAt: "2026-10-29T04:39:33.728Z"
updatedAt: "2026-10-29T04:39:54.237Z"
---
## What I did
I removed every length cap in core/src/review-deck.ts, added a core test, and pushed straight to main as **d402784**. I queued a redeploy, so d402784 should be live after it. I have not checked it on the live site.

## Findings
- **Cause.** One helper in review-deck.ts, `oneLine(s, max = 160)`, did all the cutting. The proposal approach was cut at 400 characters. Decision text in history lines and event notes were cut at 160. The title of the previous rollup was cut at 80, and the titles in the "your flags" line at 60. Each cut ended in "…".
- **Fix.** `oneLine` now only collapses whitespace to one line and never cuts. Every slide field is shown whole: approach, history notes, rollup titles and flag titles. The slide already scrolls. Whitespace stays collapsed because the approach sits inline inside the "What it is" line of the card.
- **Test.** New test in core/test/review-deck.test.ts, "the proposal slide shows a long approach whole": a 900+ character approach comes through whole on the proposal slide, with no "…".
- **Checks.** `npm run typecheck` passes. Deck tests pass: core review-deck 6/6, server review-deck 1/1, web reviewDeck + deckView 7/7.
- **Not touched:** the in-tray badge count (problem 2 in [dc_o5iz67jmoz](2026-10-29-grant-step-4-live-at-e74ae79-get-api-review-deck-a-iz67jmoz.md)).

## What I need from you
Nothing needed.
