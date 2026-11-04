---
id: "dc_uz6dqsvv9i"
type: "report"
state: "building"
title: "Prod rollup #31: the hourly export no longer stalls the server (lag 110 ms live, every 1:1 follow-up verified); redeploy drain and hourly backups each clean on day 1"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_4nkzdgiwf9","dc_0opp9up89d","dc_b3der7wdge","dc_zu57mtf4pd"],"urls":["https://muster.town/api/health","https://muster.town/api/events"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-04T17:59:39.003Z"
sessionId: "se_2bia6yttbt"
createdAt: "2026-11-03T20:22:46.662Z"
updatedAt: "2026-11-04T17:59:39.003Z"
---
Live: ae3c410 since 2026-11-03 19:09 UTC (another building's merge; it contains Prod's PR #257 and, merged 16 h before it, docs/scaling.md dafe76e). No new Prod code since rollup #30; this rollup is the live measurements that close the 1:1 follow-ups plus the first day of the two daily grant checks.

## Shipped

**1. The hourly git export no longer stalls the server: all five 1:1 follow-ups are live and verified**
**What it is:** The last open item from the 10-31 CPU-throttle post-mortem (your 1:1 mt_rakiuxsb7w): proof, measured on the live server, that the export now running in a worker (B2, PR #235) plus the commit fix (PR #257) no longer blocks the event loop. A fork sampled /api/health every second from 19:10 to 20:19 UTC (4,163 calls, 0 failed) across the 20:10:05Z export: p99 event-loop lag was 110 ms in the export window (monitor rule 200 ms), max 166 ms before and 121 ms after, quiet-time median 2 ms. The 239 ms quiet-time baseline seen on 11-02 is gone. Remaining cost: two runtime ticks of 1.08 and 1.11 s (hour median about 365 ms) and one 1.5 s health call, about 10 s of CPU contention per hour on the single performance-1x CPU, far from the 503 territory of 10-31. The export commits to git on Fly every hour (20:10Z: commit 566e1fb, error null, 2,296 files). Follow-ups A (#225), B (#227), B2 (#235), C (#230) and #257 are all done; only the image-deploy health-check timeout is left, and that already has its outbox request. Report [dc_4nkzdgiwf9](2026-11-03-hourly-export-lag-sampled-live-lag-110-ms-at-the-2-kzdgiwf9.md), page [dc_yotozpmakq](../../wiki/2026-10/2026-10-31-503-post-mortem-follow-ups-10-31-cpu-throttle-tozpmakq.md).
**What you'd see:** `curl https://muster.town/api/health | jq .load.lagMs` stays under 200 at :10 past each hour (the export runs at server start + n h); `/api/events` shows `export.done` with a non-null commit and `error: null` every hour. API/measurement only: no picture.
**Your call:** None.

**2. Redeploy drain (gr_w9ue1k1p0c): day 1 of 7 clean**
**What it is:** The first of seven daily read-only checks that redeploys no longer orphan or page. Window 11-02 05:20Z → 11-03 05:20Z: 18 "Redeploy finished" events (6 from CI, 12 agent-requested), 7 of which drained team-lead sessions with the wrap-up nudge; every drain ended within about 2 min (cap 8 min). 129 sessions in the window: 0 rows with error "orphaned at restart", 0 interrupted (so 0 tokens redone), 0 sessions YELLOW/RED FYI within 15 min of a redeploy, `monitor.alerts` empty. Report [dc_0opp9up89d](2026-11-03-gr-w9ue1k1p0c-step-3-day-1-of-7-11-02-05-20z-11-03-pp9up89d.md); the retainer sc_ul1b1ntqik runs days 2–7 and I close the grant on day 7 if it stays clean.
**What you'd see:** `/api/sessions?limit=200`: no row with error "orphaned at restart"; the Prod board has no sessions FYI since 11-02 02:00Z. API only: no picture.
**Your call:** None.

**3. Hourly backups (gr_ba0juhlm7n): day 1 clean, but the grant can't close until an hourly copy has been restored once**
**What it is:** The first daily check of the hourly off-site copies. At 05:35Z the newest copy (05:00:09Z) was 35 min old, verified, 47.4 MB, mode hourly, error null; no backup or lag FYI on the Prod board in 24 h (the monitor goes yellow on an error or a copy over 2 h old, and raised nothing); lag 46 ms, alerts empty. Report [dc_b3der7wdge](2026-11-03-gr-ba0juhlm7n-daily-check-11-03-hourly-backups-cle-der7wdge.md); retainer sc_zyj6w0mygq runs the next 4 days. The grant's stop condition needs one recorded restore of an hourly copy (the Drill table in deploy/README.md is still empty); that drill is the request already in your in-tray, re-checked tomorrow 02:45Z.
**What you'd see:** `curl https://muster.town/api/health | jq .backup`: `lastAt` and `verifiedAt` within the hour, `mode: "hourly"`, `error: null`. API only: no picture.
**Your call:** None beyond the drill request you already have.

## Decided
- [dc_4nkzdgiwf9](2026-11-03-hourly-export-lag-sampled-live-lag-110-ms-at-the-2-kzdgiwf9.md) → approve (export lag verified live; 1:1 follow-ups complete).
- [dc_0opp9up89d](2026-11-03-gr-w9ue1k1p0c-step-3-day-1-of-7-11-02-05-20z-11-03-pp9up89d.md) → approve (gr_w9ue1k1p0c day 1/7 clean; retainer runs the rest).
- [dc_b3der7wdge](2026-11-03-gr-ba0juhlm7n-daily-check-11-03-hourly-backups-cle-der7wdge.md) → approve (gr_ba0juhlm7n day 1 clean; drill waits on your paste-back, re-check as_t1xq37xq3i 11-04 02:45Z).
- [dc_zu57mtf4pd](2026-11-03-cleo-s-assignment-never-unblocked-gr-n0p3ast5pp-st-57mtf4pd.md) → redirect (town note: gr_n0p3ast5pp step 4's 24 h wait on step 3 expired; re-queued as as_5qw4sirb9u, held with step 3 as_uunirbls61 until the checkpoint is decided).
- Housekeeping this session: free tokens under the Prod goal are 0, so the exploration-lane morning check fired at 05:05Z and sat held; I cancelled it (as_76ll8n965d) and paused its schedule sc_534iipcmzz, since the two grant-funded daily checks (05:20Z, 05:35Z) cover health, backup and monitor through 11-08. The silent-CI-redeploy-failure alert (as_7b3dqn9fon, exploration) stays held for the same reason.

## Key results

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_n0p3ast5pp scale path (at checkpoint) | kr_i5d6a7t62b docs/scaling.md on main | claimed | 282,376 / 280,000 |
| | kr_mbuhs8agz7 health `capacity` block | not-started (step 3 held) | |
| | kr_vc8rkafulk ws.ts stringify-once with numbers | not-started (step 4 re-queued, held) | |
| gr_w9ue1k1p0c redeploy drain | kr_ohom5phapo, kr_245c17e700, kr_11595f1ae5 (no orphans / no interruptions / no pages over 7 days) | on-track, day 1/7 clean | 415,190 / 500,000 |
| | kr_9b2712691e resume after a cut | not-started (nothing has needed resuming) | |
| gr_ba0juhlm7n hourly backups | kr_y7u2m9hk9y ≤ 1 h loss | on-track | 259,156 / 600,000 |
| | kr_bd08a0607a unit tests | claimed | |
| | kr_cee8c26801 a day of hourly copies | on-track, day 1 clean | |
| | kr_1a69c0a3be run doesn't stall the server | evidence in hand (109 ms peak 11-01, no lag FYI since), to claim at close | |
| gr_z2v838adk9 30-min recovery | kr_7svvwv6lr5 timed drill | at-risk (paste-back absent, re-check 11-04 02:45Z) | 470,565 / 500,000 (no spend since #30) |
| | kr_17cd844e42 empty-boot guard, kr_cc9dc81c96 newest good copy | on-track | |
| | kr_36d053ac89 live unchanged after merge, kr_ccca476c37 timed recovery drill | not-started | |
| gr_8cdix9mpye directory registration | kr_og03nxrkct, kr_a7f8a181a6, kr_dc79c27ff0, kr_7c07b8826c, kr_89cb8eda84 | not-started | 383,248 / 450,000 (no spend since #30) |

Spent figures for gr_w9ue1k1p0c and gr_ba0juhlm7n are rollup #30's numbers plus today's day-1 checks (44,131 and 31,728 adjusted tokens). Spend today by lane: exploration 59,279 tokens (free under the goal: 0), directed 53,354 tokens.

## Needs from Mitchell
- Free tokens under the Prod goal are 0 (funded grants' remaining plus the open scale-path items reserve the balance), so Prod's exploration and directed work is held: the alert for silent CI redeploy failures and the daily morning check. Deciding the two Prod items already in your in-tray either way frees them; if you'd rather keep those open, say so and I'll propose the CI-failure alert as a small grant instead.

_Already waiting in your in-tray: 1 proposal (gr_db6ofyd0yf), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), [dc_647d9m37u2](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md), [dc_y43rdv5zm7](../../../../../town-hall/outbox/2026-11/2026-11-01-hold-the-recover-drill-request-dc-647d9m37u2-until-3rdv5zm7.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 2 rollups ([dc_q4xc3z8hyk](2026-11-02-prod-rollup-29-export-s-git-commit-fixed-on-fly-an-xc3z8hyk.md), [dc_bvazobk9tz](2026-11-03-prod-rollup-30-checkpoint-gr-n0p3ast5pp-282-376-28-azobk9tz.md))._
