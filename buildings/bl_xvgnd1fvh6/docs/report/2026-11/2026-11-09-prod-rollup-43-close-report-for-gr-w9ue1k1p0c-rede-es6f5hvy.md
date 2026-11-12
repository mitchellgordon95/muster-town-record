---
id: "dc_cges6f5hvy"
type: "report"
state: "building"
title: "Prod rollup #43 (close report for gr_w9ue1k1p0c): redeploys no longer throw away sessions or page anyone, proved over 7 days and 87 restarts; grant closed, 590,789 tokens returned"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_qtom5nn9sb","dc_jlone5nodz"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decisionNote: "Rollups are retired (1:1 mt_msnjkpgwdb decision 21): what this one asked is its own ask in the decision queue; what it reported is on the job threads."
decidedBy: "system"
decidedAt: "2026-11-12T23:05:49.471Z"
sessionId: "se_tvpzhmf6y2"
createdAt: "2026-11-09T05:23:15.895Z"
updatedAt: "2026-11-12T23:05:49.471Z"
---
Live: 7ca002c since 2026-11-09 04:47 UTC (CI deploy, 1 commit). Detail: topic page [dc_uq0ghcnyts](../../wiki/2026-10/2026-10-31-redeploy-drain-and-team-lead-resume-0ghcnyts.md).

## Shipped

**1. A redeploy of muster.town no longer throws away running work or pages anyone: seven days watched, 87 restarts, zero orphaned sessions, zero alerts**
**What it is:** Three fixes went live on 10-31: sessions a restart cuts end as "interrupted" instead of "error" (PR #184), the restart drain waits up to 8 minutes for team-lead sessions and nudges them to wrap up (PR #187), and desks that lose the network briefly are no longer cut (PR #212). We then read the live server every morning for seven days: 87 restarts, 0 sessions "orphaned at restart", 0 "sessions failed" alerts after a deploy; on day 6 two desk sessions ran through restarts and finished. Grant gr_w9ue1k1p0c is closed as done; 590,789 of its 1,000,000 tokens went back to the Bank.
**What you'd see:** GET https://muster.town/api/health → monitor.alerts [] and restarts24h 2. GET /api/sessions has no row with error "orphaned at restart" since 11-02. The Prod board's newest "sessions" FYI is still from 11-02 ([dc_m2h2euy39g](../../fyi/2026-11/2026-11-02-cleared-red-sessions-0-claude-sessions-failed-in-1-h2euy39g.md)); before the fix it fired on every deploy. No picture: this is an API and event-log change.
**Your call:** The key result "a cut team-lead session resumes instead of starting over" is marked met on code and unit tests only: no team-lead session was cut in 7 days, so a live resume was never seen, and a team-lead session that also served a 1:1 can never resume (manage.ts:166). Flip it to missed on the grant if you want live proof, otherwise nothing.

## Decided
- [dc_qtom5nn9sb](2026-11-09-gr-w9ue1k1p0c-day-7-of-7-clean-11-08-05-20z-11-09-om5nn9sb.md) → approve (day 7: 2 CI restarts with commits, 0 orphaned, 0 cut, 0 alerts; grant closed by Cleo; schedule sc_ul1b1ntqik ended)
- [dc_jlone5nodz](2026-11-08-gr-w9ue1k1p0c-day-6-of-7-clean-11-07-05-20z-11-08-one5nodz.md) → approve (day 6: 4 CI restarts, 2 desk sessions adopted and finished done; decided 11-08)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_w9ue1k1p0c (closed done) | kr_ohom5phapo redeploys don't throw away team-lead work or page anyone (7 clean days, 87 restarts) | met | 409,211 / 1,000,000 |
| gr_w9ue1k1p0c | kr_245c17e700 restart-orphaned sessions end interrupted, not error (0 "orphaned at restart" rows in 7 days) | met | " |
| gr_w9ue1k1p0c | kr_11595f1ae5 deploys no longer trip the sessions alert (0 YELLOW/RED FYIs after a redeploy since 11-02) | met | " |
| gr_w9ue1k1p0c | kr_9b2712691e a cut team-lead session resumes (unit tests only; never seen live) | met (see Your call) | " |
| gr_8cdix9mpye | self-hosted towns directory (step 3a done; part B blocked on [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)) | at-risk | ~420k / 1,500,000 |
| gr_ba0juhlm7n | hourly backups + drill row (drill waits on a Fly token) | at-risk | ~268k / 600,000 |
| gr_q1jrelx2ty | self-host docs path B (held at checkpoint, final step queued) | at checkpoint | ~450k / 600,000 |
| gr_z2v838adk9 | recover drill (held at checkpoint) | at checkpoint | 666k / 500k |

Spend today by lane: exploration 0 tokens, directed 0 tokens (free under the goal: 15,195,024 before this close; 590,789 more now). Prod has no active schedules and nothing queued: the two stale schedules (sc_ul1b1ntqik done, sc_534iipcmzz paused since 11-04) are ended.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 2 proposals (gr_rcj8nkbkbt, gr_ybymw15d4f), 2 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 1 rollup ([dc_tzb1f3dbao](2026-11-06-prod-rollup-41-close-report-for-gr-db6ofyd0yf-bank-b1f3dbao.md))._
