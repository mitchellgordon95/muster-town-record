---
id: "dc_nx601bgrso"
type: "report"
state: "building"
title: "Prod rollup #33 (close gr_n0p3ast5pp, 796,943 / 1,200,000): the scale-path grant is done, live as 9a119d14: /api/health has a capacity block and the WebSocket fanout stringifies each change once"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_ys38iqjp5l","dc_8kqj3u13pd","dc_scu2qa641y","dc_j59e02jlaw","dc_pesfo75mu9","dc_bvazobk9tz","dc_zq0j0km04l","dc_hbyo3dp8m2"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "stop"
decision: "pending"
sessionId: "se_qualrxbkk2"
assignmentId: "as_ta6hdtxm9q"
costUsd: 3.8056916999999997
tokens: 190285
turns: 45
createdAt: "2026-11-04T01:07:12.215Z"
updatedAt: "2026-11-04T01:07:12.215Z"
---
Live: 9a119d14 since 2026-11-04 01:00 UTC (my merge of PR #289; it also carries PR #291). Grant gr_n0p3ast5pp closed as done via close_grant: all three key results are on main and live, so this is its close report, not a checkpoint.

## Shipped

**1. Anyone can check muster.town's headroom live**
**What it is:** GET /api/health now has a `capacity` block: WebSocket clients against the 1,200 ceiling, runtime tick p95 against the 500 ms slow line, town.db MB against the volume GB, and restarts in the last 24 h. Computed in the 5 s health refresh, never on the request path. PR #289 (Cleo 1, [dc_zq0j0km04l](2026-11-04-gr-n0p3ast5pp-step-3-health-capacity-block-in-pr-2-0j0km04l.md)), merged as 9a119d14 after I fixed its dead-code CI failure. docs/scaling.md "How to check headroom live" names the same fields.
**What you'd see:** `curl https://muster.town/api/health` at 01:04 UTC: wsClients 2 / 1200, tick p95 353 ms (32 samples, right after boot), db 124.2 MB / 10.4 GB, restarts24h 3. API-only change, no picture. restarts24h counts the new "Server started" marker, so it starts from this deploy.
**Your call:** None.

**2. The WebSocket fanout stringifies each change once, not once per viewer**
**What it is:** packages/server/src/ws.ts keeps one subscription per server and hands the same string to every streaming socket (snapshot and error frames stay per socket). PR #291 ([dc_hbyo3dp8m2](2026-11-04-gr-n0p3ast5pp-step-4-ws-ts-stringifies-each-change-yo3dp8m2.md)), merged as 111e0bfd. Desk benchmark at 1,000 sockets in docs/scaling.md: 25.2 → 20.7 ms per change wall (−18 %), 12.7 → 10.5 ms CPU, event-loop lag p50 111 → 85 ms (−23 %), 0 drops. Kept though the per-change saving is just under the 20 % line, because lag (what the monitor watches) fell 23 % and the code shrinks.
**What you'd see:** Nothing visible at today's 1–2 viewers; the gain shows at hundreds. Watch item: a YELLOW ws alert (33 → 69 abnormal socket closes in 5 min, FYI [dc_xg7trks8sf](../../fyi/2026-11/2026-11-04-cleared-yellow-ws-0-websocket-errors-in-5-min-7trks8sf.md)) opened at 00:56 UTC on the first process running this change; the web client's socket code did not change in that deploy, and the current process (after two more restarts by other buildings' redeploys) sampled 0 errors at 01:04 UTC, so it clears after 5 clean samples. If ws yellows recur at restarts I will look at the shared subscription first.
**Your call:** None.

## Decided
- [dc_zq0j0km04l](2026-11-04-gr-n0p3ast5pp-step-3-health-capacity-block-in-pr-2-0j0km04l.md) → approve (step 3, PR #289; merged here as 9a119d14).
- [dc_hbyo3dp8m2](2026-11-04-gr-n0p3ast5pp-step-4-ws-ts-stringifies-each-change-yo3dp8m2.md) → approve (step 4, PR #291; merged here as 111e0bfd).
- Held merge continuations as_nx4iupm427 and as_olph0w2ny0 cancelled: both merges done by hand in this session.

## Key results
| Grant | Key result | Status | How to check | What the check showed |
|---|---|---|---|---|
| gr_n0p3ast5pp (closed, 796,943 / 1,200,000; 403,057 returned) | kr_i5d6a7t62b docs/scaling.md | claimed | docs/scaling.md on main: ≥ 6 resources with source and trigger; README links it | 8 rows, each with ceiling, live value, trigger, next fix; on main since dafe76e |
| | kr_mbuhs8agz7 capacity block | claimed | `curl https://muster.town/api/health` → capacity non-null | present at 01:04 UTC: ws 2/1200, tick p95 353/500 ms, db 124.2 MB/10.4 GB, restarts 3 |
| | kr_vc8rkafulk stringify once | claimed | ws.ts on main has no per-socket stringify of changes; before/after table in the doc; live commit contains the merge | one subscription per server (111e0bfd); table in docs/scaling.md; live 9a119d14 contains it |
| gr_ba0juhlm7n (227,428 / 600,000) | kr_y7u2m9hk9y hourly copies | on-track | health backup.lastAt < 70 min old over a day | day 1 clean ([dc_b3der7wdge](2026-11-03-gr-ba0juhlm7n-daily-check-11-03-hourly-backups-cle-der7wdge.md)); day check runs 05:35 UTC |
| | kr_bd08a0607a unit tests | claimed | npm test in packages/server green | green |
| | kr_cee8c26801 live cadence | on-track | lastAt and verifiedAt < 70 min old | day 1 clean |
| | kr_1a69c0a3be live cost | not-started | lag < 200 ms during a run | not yet sampled |
| gr_z2v838adk9 (470,565 / 500,000) | kr_7svvwv6lr5 30-min recovery | at-risk | README "Recover" drill ≤ 30 min | waits on the drill paste-back (outbox [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)) |
| | kr_17cd844e42 empty-boot guard | on-track | server test | test green on branch |
| | kr_cc9dc81c96 first-boot restore | on-track | server test | test green on branch |
| | kr_36d053ac89 live unchanged after merge | not-started | health backup.error null after redeploy | not merged yet |
| | kr_ccca476c37 timed drill | not-started | README "Recover" timestamps | waits on the paste-back |
| gr_w9ue1k1p0c (371,059 / 500,000) | kr_ohom5phapo redeploy keeps sessions | not-started | /api/sessions 7 days: no "orphaned at restart" | day 1 of 7 clean ([dc_0opp9up89d](2026-11-03-gr-w9ue1k1p0c-step-3-day-1-of-7-11-02-05-20z-11-03-pp9up89d.md)) |
| | kr_245c17e700 interrupted not error | not-started | same | day 1 clean |
| | kr_11595f1ae5 no sessions alert after deploys | not-started | Prod board 7 days | day 1 clean (today's 00:56 UTC alert was ws, not sessions) |
| | kr_9b2712691e cut session resumes | not-started | unit test plus one live redeploy during a manage session | nothing to resume yet |
| gr_8cdix9mpye (383,248 / 450,000) | all five | not-started | — | not started |

Spend today by lane: exploration 0 tokens (free under the goal: 0), directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_db6ofyd0yf), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), [dc_647d9m37u2](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md), [dc_y43rdv5zm7](../../../../../town-hall/outbox/2026-11/2026-11-01-hold-the-recover-drill-request-dc-647d9m37u2-until-3rdv5zm7.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 3 rollups ([dc_bvazobk9tz](2026-11-03-prod-rollup-30-checkpoint-gr-n0p3ast5pp-282-376-28-azobk9tz.md), [dc_uz6dqsvv9i](2026-11-03-prod-rollup-31-the-hourly-export-no-longer-stalls-6dqsvv9i.md), [dc_q5prgcfqys](2026-11-04-prod-rollup-32-ci-redeploy-failures-diagnosed-and-prgcfqys.md))._
