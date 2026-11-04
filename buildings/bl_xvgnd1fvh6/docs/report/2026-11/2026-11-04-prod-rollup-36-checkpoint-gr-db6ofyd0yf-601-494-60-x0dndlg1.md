---
id: "dc_ezx0dndlg1"
type: "report"
state: "building"
title: "Prod rollup #36 (checkpoint gr_db6ofyd0yf, 601,494 / 600,000): step 2 live (index, desk 2× tick −54 %, Bank figures unchanged), step 3 running; the live median is unmeasurable while a merge storm restarts the server every minute (prod stuck at ad27e6f, PR #338 fixes CI)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_al1adzijer","dc_g05085vk5z","dc_ows685koqz","dc_nelubafakx","dc_s6fur8t11d","dc_04orzov96w","dc_y716wgmroe","dc_wydvfzm3j5"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/304","https://github.com/mitchellgordon95/muster-town/pull/332","https://github.com/mitchellgordon95/muster-town/pull/338","https://muster.town/api/health","https://muster.town/api/bank/streams","https://muster.town/api/events"]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "pending"
sessionId: "se_5f927rnv7r"
assignmentId: "as_d8iknqjyyb"
costUsd: 4.07409125
tokens: 203705
turns: 42
createdAt: "2026-11-04T19:17:01.752Z"
updatedAt: "2026-11-04T19:17:01.752Z"
---
Live: ad27e6f, restarted 8 times between 19:01 and 19:12 UTC by no-op redeploys (last boot 19:11:53 UTC). This is the second checkpoint report for the runtime-tick grant, which crossed its 600,000 tokens at 601,494 while step 3 of 3 is running on Cleo 1.

## Shipped
**1. The Bank's debit sums use a covering index, so the tick no longer scans every debit (step 2 of 3)**
**What it is:** migration 089 adds the index `bank_debits_credit(creditId, tokens)`; no Bank code changed. test/bank-debits-index.test.ts pins every Bank figure identical with the index dropped and present. PR #304 (d5dd09b7), live in edb32010 since 17:40 UTC; reports [dc_04orzov96w](2026-11-04-gr-db6ofyd0yf-step-2-missing-creditid-index-was-th-orzov96w.md), [dc_y716wgmroe](2026-11-04-gr-db6ofyd0yf-step-2-pr-304-merged-as-d5dd09b7-on-16wgmroe.md), [dc_wydvfzm3j5](2026-11-04-gr-db6ofyd0yf-step-2-live-bank-figures-unchanged-b-dvfzm3j5.md).
**What you'd see:** Town Hall Bank: per-building durable −907,734 and credited 133,599,998 identical before and after the deploy; expectedSessionTokens 122,314 before and after. Desk bench 2×: tick p50 254 → 117 ms (−54 %), p95 309 → 170–184 ms; 1× p50 62–67 → 33–47 ms. GET /api/health load.tick: streams 1.0–1.9 ms in every sample. The live median did not fall, though: ~236 ms in the 7 min after that boot, and 181–441 ms (median 333) in my 12 samples at 19:11–19:12 UTC, taken while the server was restarted 8 times in 11 min (see item 2). The last steady reading, before step 2's deploy, was 115–118 ms. API/metrics-only change: no picture.
**Your call:** Continue, adjust or cut the grant on this checkpoint card (see Needs).

**2. Town-wide FYI: a merge storm cancelled every CI run on main, prod stayed at ad27e6f, and agents' redeploys restarted the live server 8 times for nothing**
**What it is:** 12 merges in 17 min (18:54–19:11 UTC) each cancelled the previous `ci-main` run before `promote` could fast-forward prod, so 20 commits (PRs #317, #325, #328, #331, #332, #334, #335, #322, #329, …) are not live; meanwhile Pix 1, Pix 2, Mara 1 and Nell 1 called `redeploy` after each merge, and every one restarted the server with "0 new changes" (capacity.restarts24h 43). FYI [dc_uzwcg5xw3u](../../../../town-hall/docs/fyi/2026-11/2026-11-04-do-not-call-redeploy-after-a-merge-ci-deploys-gree-wcg5xw3u.md) on every board; the three managers told. PR #338 (one line in ci.yml: cancel-in-progress only for pull requests, so main pushes queue) is open and parked on CI (as_bi5d7y217b merges it on green). The proposal gr_lvzy0yxwgd in your in-tray is the other half (redeploy itself refuses a no-op restart).
**What you'd see:** GET /api/events 19:01–19:12 UTC: eight "Redeploy finished: the server is back up with 0 new changes at ad27e6f" lines; GitHub Actions on main: 11 runs in a row "cancelled". No picture (log lines).
**Your call:** None, unless prod is still at ad27e6f when you read this: then merge PR #338 yourself, or push a green sha to `prod` by hand.

## Decided
- [dc_04orzov96w](2026-11-04-gr-db6ofyd0yf-step-2-missing-creditid-index-was-th-orzov96w.md) → approve (step 2: index found and tested, PR #304 parked on CI)
- [dc_y716wgmroe](2026-11-04-gr-db6ofyd0yf-step-2-pr-304-merged-as-d5dd09b7-on-16wgmroe.md) → approve (PR #304 merged as d5dd09b7 on green CI)
- [dc_wydvfzm3j5](2026-11-04-gr-db6ofyd0yf-step-2-live-bank-figures-unchanged-b-dvfzm3j5.md) → redirect (step 2 live, Bank figures held, live tick ~236 ms right after boot: step 3 revised to attribute it first, then the explore memo, the scaling.md bench, close or report)
- [dc_al1adzijer](2026-11-04-gr-db6ofyd0yf-funded-300k-cut-into-3-steps-step-1-1adzijer.md), [dc_g05085vk5z](2026-11-04-gr-db6ofyd0yf-step-1-expectedsession-cached-exactl-5085vk5z.md), [dc_ows685koqz](2026-11-04-gr-db6ofyd0yf-step-1-pr-302-merged-acf73450-on-gre-s685koqz.md), [dc_nelubafakx](2026-11-04-gr-db6ofyd0yf-step-1-live-bank-figure-unchanged-12-lubafakx.md) → approve (step 1; covered in rollup #35 [dc_s6fur8t11d](2026-11-04-prod-rollup-35-checkpoint-gr-db6ofyd0yf-302-503-30-fur8t11d.md), the first checkpoint, which Mitchell answered with the 300k top-up)
- Also this session: as_a818wyc7qe (PR #316 merge) cancelled and re-queued as as_zyreldmg8t because main took migration numbers 091 and 092; PR #316 renumbers to 093 first.

## Key results
Grant gr_db6ofyd0yf: 601,494 / 600,000 tokens (plan 99,567; step 1 code 113,088 + merge 19,735 + live check 21,047; step 2 code 97,810 + merge 19,601 + live check 56,327; checkpoint #1 ~95,000; step 3 ~80,000 so far on Cleo 1, still running and charged to the grant).

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_2djaq46ga6 No Bank number moves | **claimed** | core tests green in each PR's CI; /api/bank/streams expectedSessionTokens same before and after each deploy | PR #302: 6 cache tests; PR #304: index test with every figure identical; expectedSessionTokens 124,404 = 124,404 (step 1 deploy), 122,314 = 122,314 (step 2 deploy); durable −907,734 and credited 133,599,998 unchanged across step 2 |
| kr_0cbw6jb2p8 Live tick median < 110 ms, streams < 10 ms | **at-risk** | 12 health samples over 2 min, ≥ 30 min after a boot | streams 1.0–1.9 ms (met). Median: 199 (11-03) → 115–118 steady after step 1 → ~236 in the minutes after step 2's boot → 181–441 (median 333) at 19:11 UTC during 8 restarts in 11 min. No steady reading possible since 17:40 UTC. Step 3's sub-step timings (PR #332, merged fd8558cc, not live) will attribute it; its memo cuts the desk 4× p50 827 → 220 ms |
| kr_50wtkdofgc Desk p95 at 2× ≤ 250 ms, 4× ≤ 900 ms, in docs/scaling.md | on-track | docs/scaling.md tick row shows before and after | measured, not written: 2× p95 165–184 ms after step 2 (≤ 250 met on the desk), 4× p95 976 → 330 ms with step 3's memo (Cleo 1, 19:10 UTC); the row goes in step 3's PR |

Other funded grants: gr_w9ue1k1p0c days 1–2/7 clean (371,059 / 500,000); gr_ba0juhlm7n day 1 clean, drill paste-back pending (227,428 / 600,000); gr_z2v838adk9 at-risk on the drill paste-back only (487,503 / 500,000); gr_8cdix9mpye not started (383,248 / 450,000); gr_q1jrelx2ty step 1 done (public ghcr image on every green main, 156,956 / 220,000), step 2 queued. Spend today by lane: exploration 95,371 tokens (free under the goal: 2,326,964), directed 164,688 tokens.

## Needs from Mitchell
- Continue this grant with a 150,000-token top-up (on this checkpoint card). Why: one key result is claimed, the streams half of the second is met, and step 3's code exists on Cleo 1's desk with the biggest cut so far (4× tick p50 −73 %); the top-up merges it, lets CI deploy it, re-samples the live median after a quiet boot, writes the scaling.md row and closes the grant. Cut instead if the steady 115–118 ms median after step 1 is enough: then the scaling.md row and the live attribution stay unmet, and step 3's branch is dropped.

_Already waiting in your in-tray: 1 proposal (gr_lvzy0yxwgd), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), [dc_647d9m37u2](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md), [dc_y43rdv5zm7](../../../../../town-hall/outbox/2026-11/2026-11-01-hold-the-recover-drill-request-dc-647d9m37u2-until-3rdv5zm7.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 0 rollups._
