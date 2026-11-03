---
id: "dc_q4xc3z8hyk"
type: "report"
state: "building"
title: "Prod rollup #29: export's git commit fixed on Fly and verified live; tick benchmark says live p95 hits 500 ms at ~1.5× today's world; Bank overdraft is holding funded work"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_cxndxc4xwz","dc_ouyjt3u91h","dc_6epzerq5s9","dc_ys38iqjp5l","dc_8kqj3u13pd","dc_scu2qa641y"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-03T21:09:26.467Z"
sessionId: "se_krpv7bbwt1"
createdAt: "2026-11-02T18:04:07.404Z"
updatedAt: "2026-11-03T21:09:26.467Z"
---
Live: 92336d0 since 2026-11-02 18:02 UTC (contains Prod's 45be606, PR #257).

## Shipped

**1. The hourly export commits to git again on Fly**
**What it is:** PR #257 (45be606) fixed the export step that had committed nothing since 2026-11-01 03:29 UTC (commit null on every run). Verified live by Cleo 1 ([dc_cxndxc4xwz](2026-11-02-export-commit-fixed-live-d268507-at-04-42z-error-n-ndxc4xwz.md)): the first export after the deploy, at 2026-11-02 04:42 UTC, committed d268507 (2,185 files, error null); 05:42 and 06:42 UTC committed again; the 11 runs from 07:42 to 17:42 UTC report "no changes" with error null.
**What you'd see:** API-only, no picture. GET https://muster.town/api/events, the export.done events from 2026-11-02 04:42 UTC on: `commit` is a sha, `error` null. Exports fire at :42 past each hour (anchored to the 03:42 UTC boot).
**Your call:** None.

**2. Runtime tick benchmark: the live server's tick p95 crosses 500 ms at about 1.5× today's world**
**What it is:** gr_n0p3ast5pp step 1 ([dc_8kqj3u13pd](2026-11-02-gr-n0p3ast5pp-step-1-tick-benchmark-1-2-4-publishe-qj3u13pd.md), results note [dc_er6dxw6kil](../../note/2026-11/2026-11-02-tick-benchmark-1-2-4-gr-n0p3ast5pp-step-1-6dxw6kil.md)). On a desk, tick p95 was 163 ms at 1×, 473 ms at 2×, 1,841 ms at 4× the live world (fits p95 ≈ 163·k^1.75). Hot spots: Bank.expectedSession per tick, Bank.debited re-summing, freeTokensAll in the explore tick. Step 2 (docs/scaling.md with 8 resources and triggers, PR #260) is written but its merge is held by the Bank overdraft below.
**What you'd see:** API-only, no picture. One live /api/health sample at 18:00 UTC today, outside any export: tick 624 ms, lagMs 238. A single sample, no lag alert on the Prod board; the 18:42 UTC lag sample (parked, resumes in about 40 min) gives the baseline.
**Your call:** None now. A Bank.expectedSession fix touches Bank code, so it will come as a proposal, not under this grant.

## Decided
- [dc_ouyjt3u91h](2026-11-02-morning-check-11-02-health-green-hourly-backup-56-yjt3u91h.md) → approve (morning check 11-02 all green)
- [dc_6epzerq5s9](2026-11-02-export-commit-failure-pr-257-merged-as-45be606-par-pzerq5s9.md) → approve (PR #257 merged as 45be606, parked on its deploy)
- [dc_ys38iqjp5l](2026-11-02-gr-n0p3ast5pp-funded-four-chained-steps-queued-tic-38iqjp5l.md) → approve (gr_n0p3ast5pp chain of four steps queued)
- [dc_8kqj3u13pd](2026-11-02-gr-n0p3ast5pp-step-1-tick-benchmark-1-2-4-publishe-qj3u13pd.md) → approve (step 1 tick benchmark)
- [dc_scu2qa641y](2026-11-02-gr-n0p3ast5pp-step-2-docs-scaling-md-in-pr-260-8-r-u2qa641y.md) → approve (step 2 docs/scaling.md in PR #260)
- [dc_cxndxc4xwz](2026-11-02-export-commit-fixed-live-d268507-at-04-42z-error-n-ndxc4xwz.md) → approve (export fix verified live; lag sample parked as as_x0s6skwxve)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_ba0juhlm7n hourly backups | kr_y7u2m9hk9y ≤ 1 h data loss | on-track | 227,428 / 600,000 |
| gr_ba0juhlm7n | kr_bd08a0607a unit tests | claimed | |
| gr_ba0juhlm7n | kr_cee8c26801 live cadence for a day | on-track (daily check sc_zyj6w0mygq missed today: overdraft) | |
| gr_ba0juhlm7n | kr_1a69c0a3be hourly run doesn't stall | not-started | |
| gr_z2v838adk9 dead-volume recovery | kr_7svvwv6lr5 30-min recovery | at-risk (waits on the drill paste-back, outbox [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)) | 452,541 / 500,000 |
| gr_z2v838adk9 | kr_17cd844e42 empty-boot guard | on-track | |
| gr_z2v838adk9 | kr_cc9dc81c96 first-boot picks newest good copy | on-track | |
| gr_z2v838adk9 | kr_36d053ac89 live unchanged after merge | not-started | |
| gr_z2v838adk9 | kr_ccca476c37 timed drill | not-started | |
| gr_w9ue1k1p0c redeploy drain | kr_ohom5phapo no sessions lost to redeploys | not-started | 371,059 / 500,000 |
| gr_w9ue1k1p0c | kr_245c17e700 orphaned → interrupted | not-started | |
| gr_w9ue1k1p0c | kr_11595f1ae5 deploys don't trip the alert | not-started (daily check sc_ul1b1ntqik missed today: overdraft) | |
| gr_w9ue1k1p0c | kr_9b2712691e cut team-lead resumes | not-started | |
| gr_8cdix9mpye directory | kr_og03nxrkct register by DNS name | not-started | 383,248 / 450,000 |
| gr_8cdix9mpye | kr_a7f8a181a6 step 1 register/list live | not-started | |
| gr_8cdix9mpye | kr_dc79c27ff0 step 2 verify/delist | not-started | |
| gr_8cdix9mpye | kr_7c07b8826c private addresses never fetched | not-started | |
| gr_8cdix9mpye | kr_89cb8eda84 step 3 stranger town listed | not-started | |
| gr_n0p3ast5pp scale path | kr_i5d6a7t62b docs/scaling.md (due 11-05) | not-started (written, PR #260 merge held) | 248,964 / 280,000 |
| gr_n0p3ast5pp | kr_mbuhs8agz7 health capacity block (due 11-07) | not-started | |
| gr_n0p3ast5pp | kr_vc8rkafulk ws.ts stringify-once (due 11-09) | not-started | |

Today's spend by lane: exploration 93,674 tokens (free under the goal: 0), directed 21,207 tokens.

## Needs from Mitchell
1. The Bank is overdrafted (its usable balance is about 30,000 tokens short since 2026-11-02 05:20 UTC). It is holding funded-grant work: both retainers you approved last night (sc_ul1b1ntqik, sc_zyj6w0mygq) missed their first daily run, the PR #260 merge step is held, and the morning check is held for lack of free tokens. Either top up the Bank or tell me which grant or retainer to cut so the rest can run.

_Already waiting in your in-tray: 0 proposals, 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), [dc_647d9m37u2](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md), [dc_y43rdv5zm7](../../../../../town-hall/outbox/2026-11/2026-11-01-hold-the-recover-drill-request-dc-647d9m37u2-until-3rdv5zm7.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 0 rollups._
