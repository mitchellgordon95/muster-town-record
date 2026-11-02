---
id: "dc_ulx9ni4xry"
type: "report"
state: "building"
title: "Scheduled work step 1: work waiting on a time now shows as \"scheduled\", not \"blocked\" (74ea055 merged, redeploy queued); step 2 migration on PR #78 for Mitchell"
authorId: "ag_tph94skbbw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 (74ea055, PR #79) acknowledged; the live check already waits on the deploy (as_itrc4ge8zo). Step 2 is a schema migration (055), so Mitchell's approval and the end-date question go into rollup 30's Needs, not to a new assignment. The step 2 build is assigned once he answers."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T16:31:12.907Z"
sessionId: "se_1kyfwbvf5v"
assignmentId: "as_uku9y0523w"
costUsd: 3.4314409000000006
tokens: 171572
turns: 76
createdAt: "2026-10-29T16:30:49.282Z"
updatedAt: "2026-10-29T16:31:12.907Z"
---
## What I did
- **Step 1, merged:** an assignment waiting on a time is now "scheduled", not "blocked". PR https://github.com/mitchellgordon95/muster-town/pull/79 merged as **74ea055** (CI green). Redeploy queued. I haven't checked it live yet.
- **Step 2, design only:** the design and migration 055 are on draft PR https://github.com/mitchellgordon95/muster-town/pull/78 (CI green). It is **not merged**.

## Findings
**What changed in step 1:**
- **Core:** a queued assignment whose time (`waitFor {after}`) is still ahead counts as scheduled (`scheduledAt` / `townScheduled` in `core/src/blockers.ts`). `blockedBy` returns null for it, and "after" is no longer a blocked kind. That means it drops out of `/api/blocked`, the red map badge and the red lines. New public route `GET /api/scheduled` lists these assignments soonest first, with each one's run time.
- **Web:**
  - the assignment card shows a blue "scheduled" pill and "runs at <your time> · <UTC>";
  - the map shows a blue "scheduled N" badge over the agent (above the red one when it has both; hovering lists the run times, clicking opens the queue);
  - the building panel's Overview has a new **Scheduled** list.
- **Manager forks:** their "Your team" block now counts scheduled items apart from held and waiting ones.
- **`scripts/town-blockers.py`:** time waits are left out of the blocker rows and out of "Pending now", and get their own line. Run against the live event log: "Scheduled, not a blocker: 21 started on their time (created to start median 162 min); 3 scheduled now: next 2026-10-29 20:00 UTC". Those 3 match `/api/blocked` before the deploy: as_rzgy2cp5xf 20:00Z, as_0fv79mewnk 20:45Z, and an alert test at 21:20Z.
- **Places with nothing to change:** the review deck's "blocked" slides and the Town Hall's "Blocked" list are about buildings with no key results, not about assignment waits. The Dashboard never counted blocked assignments.

**Tests:**
- New core test: scheduled items come soonest first; once the time passes they are neither scheduled nor blocked; other waits stay blocked. The existing blockers test is updated, the forks test now expects "0 scheduled", and there is a new web test for the "runs at" label.
- `npm run check --fast` on this desk: typecheck passed. 8 tests timed out at the 5 s limit because the desk is slow, not because an assertion failed. All five of those files passed when rerun with a 60 s timeout. CI passed.

**Step 2 design (`docs/scheduling.md` on PR #78):**
- **The table:** one new table `schedules` (migration 055), owned by a building. It holds a UTC cron expression or "every N minutes" (at least 60), plus title, description, lane fields, pages, model, status (active / paused / ended), the next run time, the last assignment it created, and a required end date.
- **Each time it fires,** it creates one assignment on the building queue. Fires missed while the server was down collapse into one. A fire is skipped while the previous one is still queued. The lane is checked again on every fire: if it no longer holds, the schedule ends and a report goes to the in-tray.
- **Guards:** every run still ends in a report the manager reviews, and every schedule has an end date (proposed default 14 days, at most 90).
- **Where you'd see it:** a Recurring list on the building panel (Pause / Resume / Cancel), the API, and town tools `schedule` / `schedules` / `cancel_schedule`.
- The code plan is in the doc.

## What I need from you
Mitchell: please approve migration 055 (the new `schedules` table, PR #78). Also say whether a 14-day default end date (90 days at most) is right, or whether schedules should run with no end.
