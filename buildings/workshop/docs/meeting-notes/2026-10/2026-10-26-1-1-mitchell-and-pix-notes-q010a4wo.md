---
id: "dc_qdq010a4wo"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-26T19:10:13.930Z"
updatedAt: "2026-10-26T19:10:13.930Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix.

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. The Bank grant is funded and Root is on step 1 (five token counters); steps 2–5 are queued behind it. What do you need?
- **Mitchell:** oh, is that why lena and keel aren't working on their assignment queues?
- **Pix:** Partly. Two things hold them. Their Bank-grant steps (Lena 3 and 5, Keel 4) wait on Root's step 2 by design, since they need the adjusted-token field that step 2 adds. Everything else in their queues is exploration lane (wake system steps 1–3, the 6130c4e live check, the standup self-close question), and exploration is held today because the Workshop has used 9.4M of its 6.3M daily allowance. Those start by themselves when the allowance resets. If you want the wake work moving now, the fix is either to raise today's allowance or fund it as a grant; I can also reorder the grant chain so Keel's drift job runs off step 1 instead of step 2.
- **Mitchell:** ok so a few things

first when i see them blocked, i see a red "x2" which i suppose means blocked on two things. but there's no way for me to find out what those two things actually are. so lets take care of that

second, i think it would be nice to have each assignment in the queue say what it's blocked on. actually we could even make it visual, have a red line between whoever is blocked and what's blocking them in the town

third thing is i think unguided exploration should use the exploration budget. but if it's making a plan for something i told you to do or investigate, that should be separate and just run till we get a grant proposal, yeah?
- **Pix:** Yes to all three. The x2 is the count of queued assignments that can't start, and nothing shows why. Here's who takes what:

1+2 → Keel: each queued assignment in the agent panel says what it waits on (a colleague's assignment with its title and owner, a deploy sha, a decision on a report, a time, a grant at checkpoint, or "exploration allowance spent, 9.4M of 6.3M"); the red xN badge opens that list on hover/click; and on the map a red line from the blocked agent to the blocker: the colleague for an assignment wait, the Town Hall for a decision, checkpoint or allowance hold, the server door for a deploy.

3 → Lena: your reading is right. Unguided exploration stays on the allowance. Work that traces to a human ask (a 1:1 decision, a flag, a rollup reply, a human tell) runs as "directed": a manager's assign or review can name lane directed with the human doc as its source, it is never held by the allowance, it is metered in its own "directed" bucket in /api/health and rollups, and it runs until a grant proposal is filed for the KR or gap. Once that lands I re-lane the held wake-system steps (they came from our 1:1) so Keel and Lena's queues move.

Both run as directed from this meeting, so they start now. Recording.

## Decisions

1. Show what blocks a queued assignment (Mitchell, 1:1 mt_ryw7ejayvu). Today a blocked agent shows a red xN badge and nothing says why. Build: (a) in the agent panel / queue list, every queued assignment that cannot start states its reason in words: waits on assignment <title> (<owner>), waits for deploy <sha> (live is <sha>), waits for a decision on <report title>, not before <time>, grant <id> at checkpoint, or exploration allowance spent (<used> of <allowance> today, resets at <time>); (b) the red xN badge lists those N reasons on hover and on click; (c) on the map, draw a red line from the blocked agent to what blocks them: the colleague whose assignment it waits on (their body or desk), the Town Hall for a decision, checkpoint or allowance hold, the server door of the building for a deploy; one line per distinct blocker, redrawn when the queue changes. Expose the reasons in the API the panel already uses (e.g. the agent's queued assignments carry a blockedBy {kind, targetId, text}). Tests, commit to main, redeploy, verify live, report with the sha and a screenshot-level description. → Keel
2. Human-directed work does not use the exploration allowance (Mitchell, 1:1 mt_ryw7ejayvu). Rule: unguided exploration (no human source) stays on the daily exploration allowance and is held when it is spent. Work that traces to a human ask runs in lane "directed": a manager's assign, review continue/redirect and meeting decisions may name lane directed when they cite a human-authored source doc (meeting notes of a meeting with a human, a flag, a rollup reply, a human tell, a human-report); it is never held by the allowance; it is metered in its own "directed" bucket shown in GET /api/health next to the exploration numbers and in the manager rollup template; it runs until its stop condition, by default until a grant proposal is filed for the KR or gap it names. Reject lane directed without a human source (keep the current error text otherwise). Update docs/goal-directed-budgets.md (lanes section) and the manager prompt text that says managers can't create directed work. Tests, commit to main, redeploy, verify live, report with the sha. Then Pix re-lanes the held wake-system exploration assignments (as_cwg8ctj1cx, as_9mm7ee38eb, source mt_pwcpdkmdyc) as directed. → Lena

