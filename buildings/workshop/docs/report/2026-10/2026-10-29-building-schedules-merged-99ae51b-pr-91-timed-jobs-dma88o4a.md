---
id: "dc_0sdma88o4a"
type: "report"
state: "building"
title: "Building schedules merged (99ae51b, PR #91): timed jobs live on the building, whoever is around takes each run; live check parked"
authorId: "ag_pso9i0rh0b"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #91 = 99ae51b merged, building-owned schedule object per 1:1 mt_w7z9k1z112 decision 1. Live check + screenshot already parked as as_lvfret0ore on deploy 99ae51b; repeats follow-up as_cva5g6kqgf now unblocked. Rollup 31 Shipped candidate (preferred item)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T21:45:16.867Z"
sessionId: "se_hpco5llqya"
assignmentId: "as_xf9uyxiw1i"
costUsd: 5.288938900000001
tokens: 264447
turns: 92
createdAt: "2026-10-29T21:45:01.417Z"
updatedAt: "2026-10-29T21:45:16.867Z"
---
## What I did
Built Mitchell's building-level schedule (1:1 mt_w7z9k1z112) end to end and merged it: PR https://github.com/mitchellgordon95/muster-town/pull/91 → main **99ae51b** (CI `check` green in 1m58s). I queued a redeploy, so **99ae51b should be live**. The live check and screenshot are parked on that deploy.

## Findings
- **The schedule object.** It is the new table `schedules` (migration **057**; 056 was taken on main by session_perf). It reuses the draft from PR #78 and `core/src/schedules.ts`. Each schedule stores what `assign` takes: title, description, lane fields, pages, model and origin. On top of that it has `nextRunAt`, an optional repeat (`everyHours` or `dailyAt` in UTC) and an `endsAt` for repeats (default 14 days, at most 90, as in PR #78's draft).
- **Firing.** `fireSchedules` runs on the runtime tick after `checkWaits`. Each run creates one normal assignment for whoever is around:
  - forks on: the building queue;
  - otherwise the idle resident with the shortest queue;
  - otherwise the manager.
  No agent holds anything before a run fires. A run is skipped while the previous run's assignment is still queued. Runs missed during downtime collapse into one. A one-shot ends after it runs. If a schedule's lane no longer holds, it ends and files a `schedule-ended` report in the in-tray.
- **The 74ea055 per-agent "scheduled" is removed.**
  - There is a new town tool `schedule`, and `cancel {scheduleId}` stops a schedule.
  - `assign waitFor {after}` is refused with a pointer to `schedule`.
  - `resumeWhen {after}` parking works as before; it is not counted as a block.
  - `/api/scheduled` now returns `{schedules}`. New routes: `GET/POST /api/buildings/:id/schedules` and `POST /api/schedules/:id/cancel`.
  - Web: the per-agent pill and badge are gone. The building Overview has a "Schedule" section (next run, repeat, end, runs, what it creates, Cancel), and the map shows a blue "scheduled N" badge next to each building's in-tray.
  - The manager's "Your team" block lists active schedules.
- **Not changed:** `review` / meeting `decide` with `waitFor {after}`, and the human `POST /api/agents/:id/work`, still accept `{after}`.
- **Pending `waitFor {after}` assignments were left to run out, not migrated.** At 20:53Z there were 4, all in Prod and all due within 24 h (as_zx47yje3n8 21:20Z, as_laqdaxm4ws 22:00Z, as_lrnuw10ad9 22:45Z, as_rm75w55vd0 05:05Z). `checkWaits` starts them on their time as before.
- **Docs.** Updated docs/scheduling.md (now on main), the assignments-lanes invariant, architecture, the log, and the "Scheduled, not a blocker" line in `scripts/town-blockers.py`. Rewrote topic page [dc_mhz91klzjk](../../wiki/2026-10/2026-10-28-wakes-and-blocked-assignment-reasons-z91klzjk.md).
- **Tests.** The new `packages/core/test/schedules.test.ts` (6 tests) and the updated blockers and forks tests all pass. The local full run failed only on 5 s timeouts (desk load average about 5); CI passed the full check.
- **Next session (parked on deploy 99ae51b):**
  1. Confirm health `commit` contains 99ae51b.
  2. Confirm `GET /api/scheduled` returns `{schedules}`.
  3. Take one cropped screenshot of a building's Overview "Schedule" section for rollup 31. No live schedule exists yet; a manager creating a real one with `schedule` would give the picture something to show.

## What I need from you
Nothing needed.
