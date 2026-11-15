---
id: "dc_c308r7x55j"
type: "report"
state: "building"
title: "Queue health step 1: screen views and who retired each ask, PR #453 open, parked on CI"
authorId: "ag_z0hz2eplwh"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T20:46:58.678Z"
sessionId: "se_5eq0udd842"
assignmentId: "as_xzne8fwaxn"
costUsd: 1.3130585
tokens: 65653
turns: 33
createdAt: "2026-11-15T20:46:58.663Z"
updatedAt: "2026-11-15T20:46:58.678Z"
---
## What I did
Built step 1 of gr_pdja05z2f1 on branch agent/pix-2/record-the-human-s-screen-time-on-queue-, opened draft PR https://github.com/mitchellgordon95/muster-town/pull/453 (commit ee009866), parked on its CI.

## Findings
- Migration 116 `screen_views` (userId, kind, itemId, meetingId, openedAt, closedAt). New core `screen-views.ts`: `setMeetingFocus` records a view on every item change whatever the meeting phase (same item twice = one row), null closes it, the 1:1's end (done/cancelled) closes it. `screenViews()` caps a view left open at 30 min; rows are never rewritten.
- `retireAsks` already received the deciding human from every caller (grant events via humanBehind; retainer, access, captain, request); only the history entry dropped it. It now writes `by` = that user id, and moot retires keep "system".
- Live check: `/api/health` `legible.screenViews` = {views, users, open} over 14 days.
- No web change was needed: the queue's existing focus PUT is enough. I skipped the optional GET /api/asks/:id call.
- Tests: meeting-focus.test.ts gains 4 tests (A→B→null gives two closed views, same item twice gives one, non-discussing view then meeting end, 30-min cap, a fund retires with by = funder). asks, measures, ask-snapshots, planner-calibration, grant-title and meetings all pass. Typecheck shows only the chain-of-command.test.ts errors that are already on main.

## What I need from you
Nothing needed.
