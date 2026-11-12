---
id: "dc_0ljaspa411"
type: "report"
state: "building"
title: "Decision 18 planned: gr_pdja05z2f1 \"Queue health: gates, budget and the human's time\" proposed (500k, 4 steps)"
authorId: "ag_hsu02xnpw7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_msnjkpgwdb","gr_pdja05z2f1","dc_271txc8zem"],"urls":["https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Decision 18 done: gr_pdja05z2f1 (500k, 4 steps) waits in the Town Hall in-tray for Mitchell. Nothing to queue; it has its own channel."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-12T17:24:56.875Z"
sessionId: "se_d4tbl1gtqn"
assignmentId: "as_l8oklnzp57"
costUsd: 1.0719148
tokens: 53596
turns: 23
createdAt: "2026-11-12T17:24:46.360Z"
updatedAt: "2026-11-12T17:24:56.875Z"
---
## What I did
Read measures.ts, the GET /api/health `legible` route, planner.ts, seen.ts, meeting-focus.ts, the web DecisionQueue and Town health tab, and the live /api/health. Then filed the proposal gr_pdja05z2f1 against gl_join. I wrote no code. Topic page: [dc_271txc8zem](../../wiki/2026-11/2026-11-12-queue-health-gr-pdja05z2f1-1txc8zem.md).

## Findings
**The proposal: gr_pdja05z2f1** (ask 500,000 tokens; similar grants spent 300k–964k).
- **Step 1 (M):** add a `screen_views` table (an additive migration). `setMeetingFocus` writes it: it opens a view on each change and closes it on null or when the 1:1 ends. `retireAsks` records which human decided the target.
- **Step 2 (M):** a pure `queueHealth` function in core, with property tests. It computes, per ask type:
  - time on the card;
  - time from first seen to decision;
  - clarifying lines (the human's 1:1 lines while the item was open, before it was decided);
  - gates per funded grant and hold share beside budget used.
  It feeds `legible.queue` in /api/health and adds a Queue health block to the Secretary's rank brief.
- **Step 3 (M):** a "Queue health, last 14 days" section on the Town health tab, with the existing §9 measures as plain-word rows.
- **Step 4 (S):** read the live numbers after a few days of queue use and tune the thresholds.

There are four key results, due 11-20 and 11-22.

**Data missing today (checked at b9accd7a):**
- **No `seen` rows for asks.** The web never calls GET /api/asks/:id; only the mock does. `seen` also keeps only the latest open, not the first. Live, all 39 of the 39 asks retired in the last 14 days count as unread.
- **No record of what was on screen.** The 1:1 focus is overwritten on each change, with no event. It is set only while the meeting is `discussing`. Utterances don't record what was open.
- **Money, retainer, access and captain asks never count as decided.** They end as `retired` with `by: "system"` when their target is decided. So time-to-decision has no money row (live: click 72.9 h over 16, policy 2.4 h over 10, credential 40.9 h over 1).
- **The Town health tab shows none of the §9 measures.** Only the Planner's calibration reads them; the Secretary's rank run doesn't.
- **Live context:** hold share is 39 of 64 closed grants (61%), and 0 grants are at a gate now. I did not compute budget utilization; no grants list endpoint exists.

**What the proposal assumes:**
- Each view is capped at 30 minutes, because an idle open tab can't be detected.
- The warning fires when there are fewer than 0.5 gates per funded grant and more than 85% of the budget is used. Mitchell gave no numbers, so these are named constants to tune.
- A "clarifying question" is any human line in the 1:1 while the item is open, with the lines ending in "?" counted separately.
- Numbers only start at step 1's deploy, so the 14-day medians stay thin for the first two weeks.

## What I need from you
Nothing needed. The proposal waits in the Town Hall in-tray for Mitchell to fund, counter or reject.
