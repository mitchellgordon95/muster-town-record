---
id: "dc_bvazobk9tz"
type: "report"
state: "building"
title: "Prod rollup #30 (checkpoint gr_n0p3ast5pp, 282,376 / 280,000): docs/scaling.md is on main with 8 resource ceilings and triggers; the health capacity block and the ws.ts fix are not started and need a 160k top-up"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_ys38iqjp5l","dc_8kqj3u13pd","dc_scu2qa641y","dc_j59e02jlaw","dc_pesfo75mu9"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/260","https://muster.town/api/health"]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-04T17:59:38.983Z"
sessionId: "se_uillefu55n"
assignmentId: "as_fijnnjvg1f"
costUsd: 2.2018964500000004
tokens: 110095
turns: 14
createdAt: "2026-11-03T02:57:36.487Z"
updatedAt: "2026-11-04T17:59:38.983Z"
---
Live: 85498fa since 2026-11-03 02:47 UTC (Onboarding's manual.md fix). Main is dafe76e (PR #260, docs only), not deployed yet; CI ships it. This is the 100 % checkpoint report for the scale-path grant: it spent 282,376 of 280,000 tokens and finished one of its three key results.

## Shipped

**1. docs/scaling.md: the written path past muster.town's first bottlenecks**
**What it is:** One page on main that lists the 8 resources that run out first (WebSocket egress, WebSocket fanout, runtime tick, restarts, database and volume, hourly backup and export, desk slots and bill, memory), each with its measured ceiling and source doc, its live value, the number at which we act, and the next fix in order. It carries the desk tick benchmark (p95 163 / 473 / 1,841 ms at 1× / 2× / 4× today's world, so live p95 crosses the 500 ms slow-tick line at about 1.5× today's world) and three scale-out options with Fly prices (perf-2x about +$34/month, a LiteFS read replica $14–33/month each, one hosted town per Machine about $14/month). deploy/README.md links it. PR #260, merge dafe76e. Reports [dc_8kqj3u13pd](2026-11-02-gr-n0p3ast5pp-step-1-tick-benchmark-1-2-4-publishe-qj3u13pd.md) (benchmark), [dc_scu2qa641y](2026-11-02-gr-n0p3ast5pp-step-2-docs-scaling-md-in-pr-260-8-r-u2qa641y.md) (doc), [dc_pesfo75mu9](2026-11-03-pr-260-merged-dafe76e-docs-scaling-md-is-on-main-k-sfo75mu9.md) (merge).
**What you'd see:** Open docs/scaling.md on GitHub main: the resource table, the tick table, the scale-out table and a "How to check headroom live" section. One row is already past its trigger: restarts, 15 in the 24 h before 11-02 03:13Z against a trigger of 10 (the redeploy-drain grant gr_w9ue1k1p0c is the fix). Docs only: no picture.
**Your call:** None.

## Decided
- [dc_ys38iqjp5l](2026-11-02-gr-n0p3ast5pp-funded-four-chained-steps-queued-tic-38iqjp5l.md) → approve (grant funded, four chained steps queued).
- [dc_8kqj3u13pd](2026-11-02-gr-n0p3ast5pp-step-1-tick-benchmark-1-2-4-publishe-qj3u13pd.md) → approve (step 1: tick benchmark note [dc_er6dxw6kil](../../note/2026-11/2026-11-02-tick-benchmark-1-2-4-gr-n0p3ast5pp-step-1-6dxw6kil.md); the hot spots went into the doc's next-fix column and into the separate tick-cost proposal, which is in your in-tray on its own).
- [dc_scu2qa641y](2026-11-02-gr-n0p3ast5pp-step-2-docs-scaling-md-in-pr-260-8-r-u2qa641y.md) → approve (step 2: docs/scaling.md in PR #260; parked while main's CI was red on another building's file).
- [dc_j59e02jlaw](2026-11-03-pr-260-main-is-green-again-merged-main-into-the-br-9e02jlaw.md) → approve (main green again, branch updated, CI re-run).
- [dc_pesfo75mu9](2026-11-03-pr-260-merged-dafe76e-docs-scaling-md-is-on-main-k-sfo75mu9.md) → approve (PR #260 merged as dafe76e).

## Key results

This grant, 282,376 / 280,000 tokens (steps 1 and 2 cost 79,768 and 61,740; two CI waits 14,233 and 19,179 while main was red on manual.md; the rest was the funding session and this checkpoint):

| Key result | Status | How to check | What the check showed (11-03 02:55 UTC) |
|---|---|---|---|
| kr_i5d6a7t62b docs/scaling.md on main (≥ 6 resources, triggers, tick 1×/2×/4×) | claimed | docs/scaling.md on GitHub main, README links it | 8 rows, each with source doc and trigger number; deploy/README.md line 58 links it; merge dafe76e |
| kr_mbuhs8agz7 health `capacity` block | not-started | `curl https://muster.town/api/health \| jq .capacity` non-null | `capacity` is absent (commit 85498fa); step queued as as_uunirbls61, held by this checkpoint |
| kr_vc8rkafulk ws.ts stringify-once with before/after at 1,000 sockets | not-started | ws.ts on main has no per-socket stringify; doc has the numbers | ws.ts line 30 still stringifies inside the per-socket `send`; step queued as as_jquem80lht behind step 3 |

Other funded grants:

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_ba0juhlm7n hourly backups | kr_y7u2m9hk9y ≤ 1 h loss | on-track | 227,428 / 600,000 |
| | kr_bd08a0607a unit tests | claimed | |
| | kr_cee8c26801 a day of hourly copies | on-track (retainer's first run today 05:35Z) | |
| | kr_1a69c0a3be run doesn't stall the server | not-started | |
| gr_z2v838adk9 30-min recovery | kr_7svvwv6lr5 timed drill | at-risk (drill paste-back still absent, parked to 11-04) | 470,565 / 500,000 |
| | kr_17cd844e42 empty-boot guard | on-track | |
| | kr_cc9dc81c96 first-boot picks newest good copy | on-track | |
| | kr_36d053ac89 live unchanged after merge | not-started | |
| | kr_ccca476c37 timed recovery drill | not-started | |
| gr_w9ue1k1p0c redeploy drain | kr_ohom5phapo, kr_245c17e700, kr_11595f1ae5, kr_9b2712691e | not-started (daily check retainer's first run today 05:20Z) | 371,059 / 500,000 |
| gr_8cdix9mpye directory registration | kr_og03nxrkct, kr_a7f8a181a6, kr_dc79c27ff0, kr_7c07b8826c, kr_89cb8eda84 | not-started | 383,248 / 450,000 |

Spend today by lane: exploration 59,279 tokens (free under the goal: 0), directed 14,345 tokens.

## Needs from Mitchell
- Continue this checkpoint with a top-up of 160,000 tokens, or cut it. A top-up finishes the two open key results: the health `capacity` block (about 55k, Prod code only) and the ws.ts stringify-once fix with before/after numbers at 1,000 sockets on a desk-local server (about 75k, dropped if it saves under 20 %), then the close (about 20k). Both steps are already queued and start on their own when the grant continues. If you cut it, the doc stands as the one finished key result and I cancel the two queued steps.

_Already waiting in your in-tray: 1 proposal (gr_db6ofyd0yf), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), dc_647d9m37u2, dc_y43rdv5zm7, [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 1 rollup ([dc_q4xc3z8hyk](2026-11-02-prod-rollup-29-export-s-git-commit-fixed-on-fly-an-xc3z8hyk.md))._
