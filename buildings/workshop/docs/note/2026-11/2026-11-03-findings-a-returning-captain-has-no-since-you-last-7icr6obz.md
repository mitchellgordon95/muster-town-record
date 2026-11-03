---
id: "dc_w97icr6obz"
type: "note"
state: "building"
title: "Findings: a returning captain has no \"since you last reviewed\" view (explore as_okxkncoucv)"
authorId: "ag_0fxsp6r75j"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-03T02:54:45.527Z"
updatedAt: "2026-11-03T02:54:45.527Z"
---
Question: when a human who captains part of the goal tree comes back after a day, can they see what changed under their goal since they last looked, and who decided it?

## What the code says (main 335c586, read 2026-11-03)
- docs/goals.md step 4 "Built" ends with: "Left for later: the per-user review marker (`lastReviewedAt` per human, "decided by Lena")…". It was never built: a grep for lastReviewed/lastReviewedAt finds nothing in packages/*/src.
- docs/goals.md "The planning agent" says Planner's first prompt carries "an event digest since the human's last review". `Reorgs.plannerBrief` (core goal-changes.ts) builds the tree, statuses and KRs. It has no digest, because no review time is stored.
- The review deck's slide 1 (`townSlide`, core review-deck.ts ~l.310) shows the same whole-town numbers to everyone: Bank, spend by lane, desks by pillar, and a building/KR light table. It is not scoped to the viewer's subtree and has no "since" window. The in-tray and the deck do have Mine/All routing (core intray-routes.ts), so a captain's decisions are filtered, but the context around them is not.
- Agents get exactly this already: `Presence.digest(agentId, since, until)` (core presence.ts) gives a returning visitor a mailbox digest of its offline window on its first `look`. Humans have nothing like it.
- The event log has everything a digest needs: `goal.created/edited/moved/retired/owned`, `kr.updated/archived`, grant fund/close/checkpoint events, `decidedBy` on docs, goal proposals, captain requests and retainers. Each can be routed to a goal with `Goals.route`.

## Inference
- The four funded grants under gl_join (gr_bwm0iz7rwl, gr_zsm1piyqyx, gr_yu6qw3j9x5, gr_8i952perny) give a second human the rights to decide, 1:1, flag, cap and stop. None of them helps that human see what happened between visits. Once two humans steer, "who decided this, and what moved while I was away" becomes the first question, and right now the answer means reading the event log by hand.
- The cheapest form: one nullable column (users.lastReviewedAt), stamped when the human reaches the deck's last slide or presses "Mark reviewed". Plus one core function `sinceDigest(world, userId, goalId, since)` that the deck's slide 1 (scoped to the viewer's Mine subtree), the in-tray header and the Planner brief all share.

## What I don't know
- Whether Mitchell wants the stamp to be automatic (deck end) or explicit (a button). The proposal does both and keeps the earlier stamp only if the human pressed nothing.
- How noisy the digest is on a busy day. Edition 7 of Town blockers ([dc_oia5ivzayz](../../report/2026-10/2026-10-31-town-blockers-edition-7-16-47-19-34z-mitchell-36-m-a5ivzayz.md)) counted ~75k events in total, and most are presence or session noise, so the digest must allow-list event types rather than filter them out.

