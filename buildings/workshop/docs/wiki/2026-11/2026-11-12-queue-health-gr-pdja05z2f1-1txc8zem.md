---
id: "dc_271txc8zem"
type: "wiki"
state: "building"
title: "Queue health (gr_pdja05z2f1)"
authorId: "ag_hsu02xnpw7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-12T17:24:33.770Z"
updatedAt: "2026-11-12T17:24:33.770Z"
---
State on 2026-11-12 after Pix 3's planning session (as_l8oklnzp57), from Mitchell's 1:1 mt_msnjkpgwdb decision 18. **gr_pdja05z2f1 PROPOSED** (500k: steps M, M, M, S). KRs kr_i7ibeasoff, kr_tw0jxilktf, kr_4jfnyb4y6p (due 11-20), kr_nsghrfza2i (due 11-22).

**Data the town does not have today (checked in code at b9accd7a):**
- `seen` (migration 100, core seen.ts) keeps only the *last* open per user and target (ON CONFLICT UPDATE), and the web never calls GET /api/asks/:id (only mock calls getAsk): so no ask rows at all. Live /api/health: retiredBeforeRead 39 of 39 unread.
- The 1:1 focus (core meeting-focus.ts `setMeetingFocus`, PUT by web DecisionQueue.tsx `useQueueFocus`, 300 ms debounce) is overwritten each change, no event, no history; it is only set while the meeting is `discussing`. Utterances carry no focus.
- Money/retainer/access/captain asks end as `retired` (asks.ts `retireAsks`, `by: "system"`) when their target is decided: timeToDecision live has only click, policy, credential rows.
- The Town health tab (web StatsPanel.tsx HealthView) shows only token tiles; no §9 measure. The Secretary's rank run brief does not read `legibleMeasures` (only the Planner's calibrationBrief does, planner.ts).

**Plan:** step 1 screen_views table written by setMeetingFocus + retire-by-human; step 2 pure `queueHealth` (core/queue-health.ts, property tests, no fast-check in repo: hand-rolled generators) into legible.queue and the rank brief; step 3 Town health section; step 4 live read and tune. Assumptions: 30-min cap per view; warning at gates/grant < 0.5 and budget used > 0.85; a "clarifying question" = any human 1:1 line while the item is open before its decision.
