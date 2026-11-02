---
id: "dc_qfzu54biq8"
type: "report"
state: "building"
title: "Schedules step 2 merged (0a853c9, PR #92): pause/resume, end after N runs, edit, skip while running; live check parked"
authorId: "ag_t58g2348b0"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: schedules step 2 (PR #92 = 0a853c9, migration 058 paused+maxRuns) under Mitchell's 1:1 mt_w7z9k1z112 ask; live check + sc_fh7wt82tmc picture already parked as as_ytovizogrm on deploy 0a853c9. Folds into rollup 31's \"schedule object\" item; I'll state migrations 057/058 under Your call there."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T22:09:39.488Z"
sessionId: "se_ndpuqsaqbe"
assignmentId: "as_cva5g6kqgf"
costUsd: 2.1974908999999996
tokens: 109875
turns: 49
createdAt: "2026-10-29T22:09:29.396Z"
updatedAt: "2026-10-29T22:09:39.488Z"
---
## What I did
I read Pix 2's report [dc_0sdma88o4a](2026-10-29-building-schedules-merged-99ae51b-pr-91-timed-jobs-dma88o4a.md). Repeats were already there: every N hours and daily UTC times, with an end date. Several parts of the assignment were missing, so I built them and merged **PR #92: https://github.com/mitchellgordon95/muster-town/pull/92 → main 0a853c9** (CI `check` green, 2m16s). I queued a redeploy, so **0a853c9 should be live** once the restart finishes. The live check and screenshot are parked on that deploy.

## Findings
- **Already in 99ae51b:** every N hours, daily at several UTC times, an end date (`until`), catch-up of at most one missed run after a restart (`nextRunAt` is in the table), and a skip while the last run is still queued.
- **Added in 0a853c9:**
  - **Migration 058:** two new columns, `schedules.paused` and `maxRuns`. Mitchell's request in the 1:1 covers this, so it needed no separate approval.
  - **End after a count:** `repeat.times` ends a repeat after N fires. Skipped runs don't count, and the schedule ends with the reason "ran N times".
  - **Pause and resume:** a paused schedule keeps its next run time but never fires. On resume, a repeat moves to its next occurrence instead of firing the missed run late; a one-shot fires on the next tick.
  - **Edit:** `schedule {scheduleId, …}` changes the title, description, runsAt, repeat (`null` makes it a one-shot), pages or model; `paused` pauses or resumes it. The lane cannot change: cancel the schedule and make it again. The web uses the new route `POST /api/schedules/:id`. Each change logs a `schedule.edited` event. `cancel {scheduleId}` still deletes a schedule.
  - **No pile-up:** a run is now skipped while the last run's assignment is queued *or running*. Before, it was skipped only while queued. The `schedule.skipped` event says which.
  - **Building panel:** each row now shows a "paused" pill, "N times" in the repeat, a "last fired: "<title>" (queued/running/done)" line, and Pause/Resume next to Cancel. The manager's "Your team" block marks a paused schedule PAUSED.
- **Tests:** 3 new tests in `packages/core/test/schedules.test.ts`:
  - two daily times, a skip while running, and the end after 3 runs;
  - pause, resume, edit, and the lane refusal;
  - stored state surviving a reopen of the database, with 10 h of downtime giving one fire, not ten.
  
  All 9 schedule tests pass, as do blockers, waits, visitors and v12. Full typecheck is green. Locally the server suite failed only on 5 s timeouts under desk load, a different test each run; CI passed the full check.
- **Docs:** docs/scheduling.md is updated, and topic page [dc_mhz91klzjk](../../wiki/2026-10/2026-10-28-wakes-and-blocked-assignment-reasons-z91klzjk.md) is rewritten.
- **Next session (parked on deploy 0a853c9):**
  1. Confirm the health `commit` contains 0a853c9.
  2. Confirm `GET /api/scheduled` rows carry `paused` and `maxRuns`.
  3. Take one cropped screenshot (≤300 px tall) of the live repeating schedule sc_fh7wt82tmc (Workshop, daily 19:30 UTC) in the Overview "Schedule" section, for rollup 31.

## What I need from you
Nothing needed.
