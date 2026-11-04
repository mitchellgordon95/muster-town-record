---
id: "dc_q5prgcfqys"
type: "report"
state: "building"
title: "Prod rollup #32: CI redeploy failures diagnosed and fixed (FETCH_HEAD race, 3 of 30 runs) with a redeploy-failed alert, live as 1826430; scale-path grant continued at 500k, steps 3 and 4 running"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_shjpotcro8","dc_dj501thwsh","dc_snjtbqs8xn","dc_6ojrt3o7mk"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/285","https://muster.town/api/health"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-04T17:59:39.020Z"
sessionId: "se_vi8l2me0e4"
createdAt: "2026-11-04T00:24:25.925Z"
updatedAt: "2026-11-04T17:59:39.020Z"
---
Live: db2b9dd since 2026-11-03 23:43 UTC (another building's merge; it contains Prod's PR #285, 1826430, live since 22:38 UTC).

## Shipped

**1. CI redeploys no longer fail at random, and a failed one now pages you**
**What it is:** Three of the last 30 CI redeploys (11-02 03:57Z, 11-03 18:26Z and 19:25Z) died with git's "Cannot rebase onto multiple branches" (exit 128), which left main undeployed for up to 3 h each time. Cause: a race inside one checkout between the runtime's 5-minute code fetch (`packages/runtime/src/code.ts`), which rewrites FETCH_HEAD, and the redeploy's `git pull --rebase origin prod`, which reads it. Reproduced on a desk: 48 of 60 concurrent runs failed; with `--no-write-fetch-head` on the code fetch, 0 of 60. That one flag is the fix. Same PR adds a `redeploy-failed` monitor metric (`packages/server/src/monitor.ts`): it goes red when the latest finished redeploy ended failed or aborted, raises the usual alert event and Prod FYI, clears after a later run reaches done, and Wright's pinger forwards it so you get one text. 32 monitor tests pass; a row in deploy/README.md's Monitoring table. PR #285, merged as 1826430; CI's own redeploy of the merge shipped it without a manual redeploy (so it did not hit the race). Verified live at 22:38Z: health commit = 1826430, `monitor.alerts` = []. Reports [dc_shjpotcro8](2026-11-03-failed-ci-redeploys-diagnosed-fetch-head-race-3-of-jpotcro8.md), [dc_dj501thwsh](2026-11-03-pr-285-merged-as-1826430-fetch-head-race-fix-redep-501thwsh.md), [dc_snjtbqs8xn](2026-11-03-pr-285-live-api-health-commit-1826430-monitor-samp-jtbqs8xn.md).
**What you'd see:** `curl https://muster.town/api/health | jq .monitor.alerts` is `[]`; if a CI redeploy ever fails again, a `redeploy-failed` alert appears there within a minute, with a Prod FYI naming the failed step and who requested the run. API/monitor only: no picture.
**Your call:** None.

## Decided
- [dc_shjpotcro8](2026-11-03-failed-ci-redeploys-diagnosed-fetch-head-race-3-of-jpotcro8.md) → approve (diagnosis + fix + alert, PR #285 opened).
- [dc_dj501thwsh](2026-11-03-pr-285-merged-as-1826430-fetch-head-race-fix-redep-501thwsh.md) → approve (PR #285 merged as 1826430 after green CI; live verify parked).
- [dc_snjtbqs8xn](2026-11-03-pr-285-live-api-health-commit-1826430-monitor-samp-jtbqs8xn.md) → approve (1826430 live, monitor green, no redeploy-failed alert; chain done).
- [dc_6ojrt3o7mk](2026-11-04-grant-gr-n0p3ast5pp-adjusted-500-000-tokens-jrt3o7mk.md) → approve (gr_n0p3ast5pp continued at 500,000 per your town-hall decision; step 3 as_uunirbls61 is running on a fork since 00:21Z, step 4 as_5qw4sirb9u follows; about 107k tokens remain for both, so a second checkpoint is possible).

## Key results

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_n0p3ast5pp scale path (continued 00:21Z) | kr_i5d6a7t62b docs/scaling.md on main | claimed | 392,471 / 500,000 |
| | kr_mbuhs8agz7 health `capacity` block | in progress (step 3 running) | |
| | kr_vc8rkafulk ws.ts stringify-once with numbers | not-started (step 4 queued) | |
| gr_w9ue1k1p0c redeploy drain | kr_ohom5phapo, kr_245c17e700, kr_11595f1ae5 (7 clean days) | on-track, day 1/7 clean; day 2 fires 05:20Z | 415,190 / 500,000 |
| | kr_9b2712691e resume after a cut | not-started (nothing has needed resuming) | |
| gr_ba0juhlm7n hourly backups | kr_y7u2m9hk9y ≤ 1 h loss, kr_cee8c26801 a day of hourly copies | on-track, day 1 clean; day 2 fires 05:35Z | 259,156 / 600,000 |
| | kr_bd08a0607a unit tests | claimed | |
| | kr_1a69c0a3be run doesn't stall the server | evidence in hand, to claim at close | |
| gr_z2v838adk9 30-min recovery | kr_7svvwv6lr5 timed drill | at-risk (drill paste-back absent; re-check 02:45Z) | 470,565 / 500,000 (no spend since #30) |
| | kr_17cd844e42, kr_cc9dc81c96 | on-track | |
| | kr_36d053ac89, kr_ccca476c37 | not-started | |
| gr_8cdix9mpye directory registration | kr_og03nxrkct, kr_a7f8a181a6, kr_dc79c27ff0, kr_7c07b8826c, kr_89cb8eda84 | not-started | 383,248 / 450,000 (no spend since #30) |

Spent figures other than gr_n0p3ast5pp's are rollup #31's (no grant spend since, the daily checks fire after 05:00Z). Spend today by lane: exploration 0 tokens (free under the goal: 0 at last read), directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_db6ofyd0yf), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), [dc_647d9m37u2](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md), [dc_y43rdv5zm7](../../../../../town-hall/outbox/2026-11/2026-11-01-hold-the-recover-drill-request-dc-647d9m37u2-until-3rdv5zm7.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 2 rollups ([dc_bvazobk9tz](2026-11-03-prod-rollup-30-checkpoint-gr-n0p3ast5pp-282-376-28-azobk9tz.md), [dc_uz6dqsvv9i](2026-11-03-prod-rollup-31-the-hourly-export-no-longer-stalls-6dqsvv9i.md))._
