---
id: "dc_97uh3xa84m"
type: "report"
state: "building"
title: "Prod rollup #34: gr_db6ofyd0yf step 1 live (Bank figure unchanged, streams phase 32–43 → ~1.3 ms, live tick 148 → 132 ms); steps 2–3 queued"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_nelubafakx","dc_ows685koqz","dc_g05085vk5z","dc_ven7cfjhqa","dc_zrym03et3g","dc_duia4kfhai"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-04T17:59:39.053Z"
sessionId: "se_9p3j7fqe3z"
createdAt: "2026-11-04T16:36:18.659Z"
updatedAt: "2026-11-04T17:59:39.053Z"
---
Live: acf73450 since 2026-11-04 16:30 UTC (PR #302, ours).

## Shipped
**1. The Bank's expected-session figure is now cached exactly (gr_db6ofyd0yf step 1)**
**What it is:** `Bank.expectedSession` is memoized (token columns only, keyed by building + newest ended work session) so the tick no longer recomputes it every second. PR #302 (acf73450). Reports [dc_g05085vk5z](2026-11-04-gr-db6ofyd0yf-step-1-expectedsession-cached-exactl-5085vk5z.md), [dc_ows685koqz](2026-11-04-gr-db6ofyd0yf-step-1-pr-302-merged-acf73450-on-gre-s685koqz.md), [dc_nelubafakx](2026-11-04-gr-db6ofyd0yf-step-1-live-bank-figure-unchanged-12-lubafakx.md).
**What you'd see:** Town Hall Bank, `expectedSessionTokens` = 124,404 before and after the deploy (948 → 949 samples): the figure did not move. /api/health tick: streams phase 31.8–42.6 ms → 1.1–1.6 ms; live median tick 148 ms (137–163) → 131.5 ms (116–181) over 24 samples, 0 errors. On the desk bench the tick fell 48 %. API/metrics-only change: no picture.
**Your call:** None. kr_0cbw6jb2p8's streams part (< 10 ms) is met; its median part (< 110 ms) is ~22 ms short, so step 2 (sum debits per credit in one GROUP BY; the work phase is 51–66 ms of the tick) is queued as as_qizum6vt19 and step 3 (one freeTokensAll per explore tick; explore phase 35–53 ms; then the 1×/2×/4× bench into docs/scaling.md and close) follows.

## Decided
- [dc_g05085vk5z](2026-11-04-gr-db6ofyd0yf-step-1-expectedsession-cached-exactl-5085vk5z.md) → approve (step 1 PR open, exact cache, desk tick −48 %)
- [dc_ows685koqz](2026-11-04-gr-db6ofyd0yf-step-1-pr-302-merged-acf73450-on-gre-s685koqz.md) → approve (PR #302 merged on green CI, parked for live check)
- [dc_nelubafakx](2026-11-04-gr-db6ofyd0yf-step-1-live-bank-figure-unchanged-12-lubafakx.md) → approve (live check: figure unchanged, median 148 → 132 ms)
- [dc_ven7cfjhqa](2026-11-04-recover-drill-dc-6gnk7y16y1-still-no-paste-back-on-n7cfjhqa.md) → approve (gr_db6ofyd0yf funded: step 1 assigned)
- [dc_zrym03et3g](2026-11-04-gr-w9ue1k1p0c-step-3-day-2-of-7-11-03-05-20z-11-04-ym03et3g.md) → approve (gr_w9ue1k1p0c day 2/7 clean: 0 orphaned, 1 interrupted = Nell's se_51f01dqh7j cut by the 22:38Z redeploy, resume not yet confirmed)
- [dc_duia4kfhai](2026-11-04-gr-ba0juhlm7n-daily-check-11-04-hourly-backups-cle-ia4kfhai.md) → approve (gr_ba0juhlm7n day 1 of hourly backups clean)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_db6ofyd0yf | kr_2djaq46ga6 Bank figure identical after memoization | on-track (step 1 live: 124,404 unchanged) | step 1 of 3 spent (figure on the grant) / 300,000 |
| gr_db6ofyd0yf | kr_0cbw6jb2p8 streams < 10 ms, median tick < 110 ms | on-track (streams met at ~1.3 ms; median 132 ms, steps 2–3 pending) | same grant |
| gr_w9ue1k1p0c | kr_ohom5phapo / kr_245c17e700 / kr_11595f1ae5 (7 clean redeploy days) | on-track, day 2/7; daily retainer sc_ul1b1ntqik held until its 45k/run is approved | see grant |
| gr_w9ue1k1p0c | kr_9b2712691e (interrupted sessions resume) | at-risk until se_51f01dqh7j's resume is confirmed | see grant |
| gr_ba0juhlm7n | hourly off-site backups, day 1 clean; restore drill paste-back pending (outbox [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)) | on-track / at-risk on the paste-back | see grant |
| gr_z2v838adk9 | kr_7svvwv6lr5 | at-risk on the drill paste-back only | 487,503 / 500,000 |
| gr_8cdix9mpye | not started | not-started | 383,248 / 450,000 |

Spend today by lane: exploration 39,603 tokens (free under the goal: 0), directed 149 tokens; grant spend is on each grant.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_q1jrelx2ty), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), dc_647d9m37u2, dc_y43rdv5zm7, [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 4 rollups ([dc_bvazobk9tz](2026-11-03-prod-rollup-30-checkpoint-gr-n0p3ast5pp-282-376-28-azobk9tz.md), [dc_uz6dqsvv9i](2026-11-03-prod-rollup-31-the-hourly-export-no-longer-stalls-6dqsvv9i.md), [dc_q5prgcfqys](2026-11-04-prod-rollup-32-ci-redeploy-failures-diagnosed-and-prgcfqys.md), [dc_nx601bgrso](2026-11-04-prod-rollup-33-close-gr-n0p3ast5pp-796-943-1-200-0-601bgrso.md))._
