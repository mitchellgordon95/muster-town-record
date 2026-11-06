---
id: "dc_s6fur8t11d"
type: "report"
state: "building"
title: "Prod rollup #35 (checkpoint gr_db6ofyd0yf, 302,503 / 300,000): step 1 live cut the streams phase 32–43 → ~1.3 ms and the live tick 148 → ~115 ms; the Bank figure held; 200k more finishes steps 2–3 (median < 110 ms, scaling.md row)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_al1adzijer","dc_g05085vk5z","dc_ows685koqz","dc_nelubafakx"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/302","https://muster.town/api/health","https://muster.town/api/bank/streams"]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-04T18:26:07.653Z"
sessionId: "se_mfvhhep7m9"
assignmentId: "as_vl9i1qaxa4"
costUsd: 1.89276585
tokens: 94638
turns: 17
createdAt: "2026-11-04T16:43:55.754Z"
updatedAt: "2026-11-04T18:26:07.653Z"
---
Live: acf73450 since 2026-11-04 16:30 UTC (PR #302, ours). This is the checkpoint report for the runtime-tick grant, which crossed its 300,000 tokens at 302,503 while step 2 of 3 was running.

## Shipped
**1. The Bank's expected-session figure is cached exactly, so the tick no longer recomputes it (step 1 of 3)**
**What it is:** `Bank.expectedSession` reads only the token columns and caches the result, keyed by one aggregate row (count, newest end, token sum) over the 7-day window; a session ending, settling or leaving the window rebuilds it. Six tests keep the old computation as the oracle and pin Bank.available, balance and freeTokensAll identical cold and warm. The tick bench is now in the repo (scripts/stress/tick-bench.mts). PR #302 (acf73450); reports [dc_al1adzijer](2026-11-04-gr-db6ofyd0yf-funded-300k-cut-into-3-steps-step-1-1adzijer.md) (plan), [dc_g05085vk5z](2026-11-04-gr-db6ofyd0yf-step-1-expectedsession-cached-exactl-5085vk5z.md), [dc_ows685koqz](2026-11-04-gr-db6ofyd0yf-step-1-pr-302-merged-acf73450-on-gre-s685koqz.md), [dc_nelubafakx](2026-11-04-gr-db6ofyd0yf-step-1-live-bank-figure-unchanged-12-lubafakx.md).
**What you'd see:** Town Hall Bank: `expectedSessionTokens` 124,404 before and after the deploy (948 → 949 samples); 123,877 at 16:42 UTC after 9 work sessions ended, which is the cache rebuilding as designed. GET /api/health load.tick: streams phase 31.8–42.6 ms → 1.1–1.9 ms; median tick 199 ms (11-03) → 148 ms (just before) → ~115 ms (110–133 over 6 samples at 16:41–16:42 UTC, 11 min after boot). Desk bench at 1×: tick p50 −48 %. API/metrics-only change: no picture.
**Your call:** Continue, adjust or cut the grant on its checkpoint card (see Needs).

## Decided
- [dc_al1adzijer](2026-11-04-gr-db6ofyd0yf-funded-300k-cut-into-3-steps-step-1-1adzijer.md) → approve (plan: 3 steps, stop rules)
- [dc_g05085vk5z](2026-11-04-gr-db6ofyd0yf-step-1-expectedsession-cached-exactl-5085vk5z.md) → approve (step 1 PR open, exact cache, desk tick −48 %)
- [dc_ows685koqz](2026-11-04-gr-db6ofyd0yf-step-1-pr-302-merged-acf73450-on-gre-s685koqz.md) → approve (PR #302 merged on green CI)
- [dc_nelubafakx](2026-11-04-gr-db6ofyd0yf-step-1-live-bank-figure-unchanged-12-lubafakx.md) → approve (live check: figure unchanged, median 148 → 132 ms at 2–4 min after boot)

## Key results
Grant gr_db6ofyd0yf: 302,503 / 300,000 tokens (plan 99,567; step 1 code 113,088; merge 19,735; live check 21,047; step 2 ~49,000 so far on Cleo 1, still running).

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_2djaq46ga6 No Bank number moves | **claimed** | core tests green in PR CI; /api/bank/streams expectedSessionTokens same before and after the deploy | PR #302 CI green with expected-session-cache.test.ts (6 tests); 124,404 before = 124,404 after at 16:31 and 16:35 UTC; moved to 123,877 only after 9 sessions ended (allowed) |
| kr_0cbw6jb2p8 Live tick median < 110 ms, streams < 10 ms | on-track | 12 health samples over 2 min: median ms < 110, phases.streams < 10 | streams 1.1–1.9 ms (met); median 110–133 ms (~115) at 16:41–16:42 UTC, ~5 ms short; work phase 45–53 ms (step 2) and explore phase 37–50 ms (step 3) remain |
| kr_50wtkdofgc Desk p95 at 2× ≤ 250 ms, 4× ≤ 900 ms in docs/scaling.md | not-started | docs/scaling.md tick row shows before and after | row still shows only before (163/473/1,841 ms); 1× p95 fell 180–204 → 101–124 ms on the desk with step 1, 2×/4× not run yet (step 3) |

Other funded grants, unchanged since rollup #34: gr_w9ue1k1p0c day 2/7 clean (371,059 / 500,000); gr_ba0juhlm7n day 1 clean, drill paste-back pending (227,428 / 600,000); gr_z2v838adk9 at-risk on the drill paste-back only (487,503 / 500,000); gr_8cdix9mpye not started (383,248 / 450,000). Spend today by lane: exploration 39,603 tokens (free under the goal: 0), directed 149 tokens.

## Needs from Mitchell
- Continue this grant with a 200,000-token top-up (on the checkpoint card this report is attached to). Why: step 1 delivered what the finding predicted (streams phase −96 %, Bank figure untouched), one key result is claimed and the median is ~5 ms from its target; step 2's code and tests are already done on Cleo 1 and its PR lands under the town merge rule, but step 3 (the explore phase, the 2×/4× bench into docs/scaling.md, the close) is held until you decide. Cut instead if a median of ~115 ms and streams at ~1.3 ms is enough for you: then only the scaling.md row stays unmet.

_Already waiting in your in-tray: 1 proposal (gr_q1jrelx2ty), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), dc_647d9m37u2, dc_y43rdv5zm7, [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 5 rollups ([dc_bvazobk9tz](2026-11-03-prod-rollup-30-checkpoint-gr-n0p3ast5pp-282-376-28-azobk9tz.md), [dc_uz6dqsvv9i](2026-11-03-prod-rollup-31-the-hourly-export-no-longer-stalls-6dqsvv9i.md), [dc_q5prgcfqys](2026-11-04-prod-rollup-32-ci-redeploy-failures-diagnosed-and-prgcfqys.md), [dc_nx601bgrso](2026-11-04-prod-rollup-33-close-gr-n0p3ast5pp-796-943-1-200-0-601bgrso.md), [dc_97uh3xa84m](2026-11-04-prod-rollup-34-gr-db6ofyd0yf-step-1-live-bank-figu-uh3xa84m.md))._
