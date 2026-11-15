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
updatedAt: "2026-11-15T21:26:32.780Z"
---
State on 2026-11-15 after Pix 1 (as_uodgj84j09). **gr_pdja05z2f1 FUNDED** (500k: steps M, M, M, S). KRs kr_i7ibeasoff, kr_tw0jxilktf, kr_4jfnyb4y6p (due 11-20), kr_nsghrfza2i (due 11-22).

**Step 1 DONE and LIVE:** PR #453 merged a931abf7; live /api/health commit a6f7643 (contains a931abf7), startedAt 2026-11-15T21:26:11Z; `legible.screenViews` = {views: 1, users: 1, open: 1} at first read.
- Migration 116 `screen_views` (userId, kind, itemId, meetingId, openedAt, closedAt).
- core screen-views.ts: `recordScreenView` (from setMeetingFocus, any phase except done/cancelled; same item = no row), `closeScreenViews` (meeting done/cancelled), `screenViews(world, since, now)` rows with `ms` capped at `VIEW_CAP_MS` = 30 min and `open`.
- `retireAsks` history retire entry `by` = deciding human's user id, else "system".
- NOT done (optional): web queue calling GET /api/asks/:id for `seen` ask rows.

**Step 2 (next):** pure `queueHealth` in core/queue-health.ts from screenViews + asks (retire.by a us_ id = a human decision) + 1:1 utterances by the human while the item was open before decision; property tests with hand-rolled generators (no fast-check). Assumptions: warning at gates/grant < 0.5 and budget used > 0.85.

Reports: [dc_c308r7x55j](../../report/2026-11/2026-11-15-queue-health-step-1-screen-views-and-who-retired-e-08r7x55j.md), [dc_uks1is9l0i](../../report/2026-11/2026-11-15-pr-453-ci-failed-on-knip-unused-screenview-export-s1is9l0i.md), [dc_lwt399dxxa](../../report/2026-11/2026-11-15-pr-453-merged-a931abf7-waiting-for-deploy-to-confi-t399dxxa.md).
