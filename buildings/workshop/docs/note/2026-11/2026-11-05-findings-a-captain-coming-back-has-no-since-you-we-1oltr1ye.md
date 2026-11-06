---
id: "dc_hd1oltr1ye"
type: "note"
state: "building"
title: "Findings: a captain coming back has no \"since you were last here\" view of their goals"
authorId: "ag_n4r47m21p7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-05T20:46:58.449Z"
updatedAt: "2026-11-05T20:46:58.449Z"
---
Exploration as_hxs23sfmfw (Pix 1), 2026-11-05, main at live f318ec8 (GET /api/health 20:46:10Z). Question: once a second human captains a goal (gr_bwm0iz7rwl), what do they see when they come back?

## What the code says (main)
- **Routing per captain is built**: in-tray Mine/All (`core/intray-routes.ts`, defaultView "mine" for a non-admin captain), Fund/Counter/Reject on grants in their subtree, 1:1s with managers there (docs/goals.md "Steering the buildings under their goal"), goal Spend (`core/goal-spend.ts`, Bank Spend by goal).
- **The "since your last review" half of the design is not built.** docs/goals.md "Review cadence and the deck": slide 1 should carry "tree changes since your last review"; "Each human has their own `lastReviewedAt`. An item decided by another human disappears from your in-tray, and the next deck notes 'decided by Lena'." Step 4 notes: "Left for later: the per-user review marker (`lastReviewedAt` per human, "decided by Lena")". `grep lastReviewedAt` over packages/*/src: 0 hits.
- **Slide 1 is town-wide** (`core/review-deck.ts` ~355-382: Bank, spend today by lane, desks by pillar, decisions count, building lights). Nothing scoped to the viewer's captained subtrees, nothing windowed by their last visit.
- **The digest card is town-wide** (`core/secretary.ts`): "Shipped since last digest" is since the last *card*, not since a given human last looked; one card for everyone.
- Only `lastSeenAt` exists (presence.ts, stamped on agent calls) — a presence stamp, not a review marker.

## Live town
- Captains today (GET /api/goals): only `gl_town` → Mitchell. So every route ends at him; the gap bites the moment gr_bwm0iz7rwl's "Ask to captain" lets a second human own a node.

## Inference
A stranger who captains, say, "Make Muster Town beautiful and intuitive" returns after two days to an in-tray of Mine rows with no sense of what changed under their goal: which rollups landed, which grants were funded/closed (and by whom), which key results went met/missed, what it spent. Steering needs that one paragraph. It also helps Mitchell now (slide 1 has no "since").

## Not known
- Whether a second human has ever opened the deck (no per-user marker to tell).
- Whether "since last review" should key on deck open, in-tray open, or an explicit "mark reviewed" press (proposal: in-tray/deck open, with the marker moved on leave).
