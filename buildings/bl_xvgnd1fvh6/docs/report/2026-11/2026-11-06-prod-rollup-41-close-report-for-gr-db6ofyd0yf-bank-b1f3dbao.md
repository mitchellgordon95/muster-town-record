---
id: "dc_tzb1f3dbao"
type: "report"
state: "building"
title: "Prod rollup #41 (close report for gr_db6ofyd0yf): Bank read paths memoized, live tick 199 → 73 ms, 1,029,156 tokens back; the self-host image now restores a town from backup on first boot (its last docs step is held at a checkpoint); drains clean 4 of 7 days, no no-op restart in day 1"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_o6nmfoaenu","dc_hljji3rohh","dc_wkfc4gd3ay","dc_rw6hbqfe3z","dc_zek4m79opw","dc_yy2psi1vd0","dc_z92lsjjzdl","dc_4sdkoccnmr","dc_xaeg9mmvmi","dc_9dvyd0hezy","dc_xbiaxit5pr","dc_ho7hfbjs99","dc_ig0clc8awx","dc_c11nq5dr2m","dc_vvr35qv8ye","dc_wewt9vcx6v","dc_j61644eaiw"],"urls":["https://muster.town/api/health","https://github.com/mitchellgordon95/muster-town/pull/340","https://github.com/mitchellgordon95/muster-town/pull/392","https://github.com/mitchellgordon95/muster-town/actions/runs/42166369737"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_upp2q4oix7"
createdAt: "2026-11-06T06:07:47.783Z"
updatedAt: "2026-11-06T06:07:47.783Z"
---
Live: 24984fc since 2026-11-06 05:21 UTC, deployed by CI. This is the close report for the runtime-tick grant gr_db6ofyd0yf (closed as done this session, 970,844 of 2,000,000 spent).

## Shipped

**1. Bank read paths memoized: the server tick is 73 ms, down from 199 ms (grant gr_db6ofyd0yf closed as done)**
**What it is:** The world tick used to recompute Bank figures (expected session tokens, streams, free tokens) from scratch every second. Four PRs cached them exactly (#302, #304 with migration 089, #332 sub-step timings in /api/health, #340 tick memo), with cache-equivalence tests in CI. The grant is closed with its three key results met and 1,029,156 unspent tokens back in the Bank. Reports [dc_o6nmfoaenu](2026-11-06-gr-db6ofyd0yf-step-4-live-tick-median-73-ms-was-19-nmfoaenu.md), [dc_hljji3rohh](2026-11-06-gr-db6ofyd0yf-step-4-f7a22677-is-live-boot-05-06-4-jji3rohh.md); page [dc_ur1qzaxafp](../../wiki/2026-11/2026-11-03-runtime-tick-cost-gr-db6ofyd0yf-1qzaxafp.md).
**What you'd see:** API only, no picture. GET https://muster.town/api/health `load.tick.last`: 30 samples at 06:02–06:04Z gave a median of 73 ms (min 68, max 164) against 199 ms (183–220) on 11-03 and 117 ms before PR #340; the streams phase is 1.4 ms (max 12). The Bank's expectedSessionTokens was 124,404 after the deploy and 124,835 before it (it drifts with sessions).
**Your call:** None: the grant is closed as done; flip a key result to missed on gr_db6ofyd0yf if the live numbers don't satisfy you.

**2. The self-host image restores a town from its backup on first boot, and CI proves it before every push**
**What it is:** Every green push to main now builds and pushes ghcr.io/mitchellgordon95/muster-town:prod (plus a :<sha> tag) only after booting the published compose, taking a verified backup, and restoring it into a second empty town. The last step of grant gr_q1jrelx2ty, a docs-only PR (#392) that makes docs/self-host.md path B pull that image, is written and green-waiting but its assignment is held: the grant reached its checkpoint. Report [dc_wkfc4gd3ay](2026-11-06-gr-q1jrelx2ty-step-3-confirmed-on-main-backup-rest-fc4gd3ay.md); page [dc_55z71al37g](../../wiki/2026-11/2026-11-04-self-host-image-gr-q1jrelx2ty-z71al37g.md).
**What you'd see:** API only, no picture. GitHub main run 42166369737 (24984fc): the smoke log shows a backup verified at 05:11:12Z (34,448 bytes) and `[restore] town/2026-11-06T05.db.gz.enc: ok, 3 agents` in town2. `docker pull ghcr.io/mitchellgordon95/muster-town:prod` anonymously gives digest sha256:704e1364…, the same as :24984fc6….
**Your call:** Continue gr_q1jrelx2ty at its checkpoint (about 150,000 more is enough: one session merges PR #392 and closes it) or cut it, in which case the docs PR merges under exploration and its second key result stays unclaimed.

**3. Restarts drain cleanly (day 4 of 7) and no restart has been a no-op since the guard went live (day 1 of 3); the directory's SSRF guard is proven live**
**What it is:** The daily reads under the redeploy-drain and no-op-restart grants, plus the directory's step 3a. Drain day 4 (11-05 05:20Z → 11-06 05:20Z): 25 restarts, 0 sessions orphaned, all 12 team-lead sessions told to finish did so in 3–72 s; the 6 cut sessions were all serving a 1:1 (answered through a drain on purpose). No-op day 1: 14 restarts, every one a CI deploy carrying 1–10 commits, 0 no-op, but restarts24h was 22 at 04:31Z, over the < 20 bar in the grant's third key result, because merges land that often. Directory: 5 hosts pointing at private or Fly-internal addresses were refused inside the lookup on the live server, 79/79 tests. Reports [dc_zek4m79opw](2026-11-06-gr-w9ue1k1p0c-day-4-of-7-clean-11-05-05-20z-11-06-k4m79opw.md), [dc_yy2psi1vd0](2026-11-06-gr-lvzy0yxwgd-day-1-read-14-restarts-since-the-gua-2psi1vd0.md), [dc_z92lsjjzdl](2026-11-06-gr-8cdix9mpye-step-3a-live-ssrf-check-passes-on-mu-2lsjjzdl.md).
**What you'd see:** API only, no picture. GET /api/health `capacity.restarts24h` (25 at 05:20Z) and `monitor.alerts` = []; /api/events since id 131355 has no "nothing new on prod" event yet (nobody asked for a no-op redeploy). GET /api/directory shows 5 pending *.nip.io / sslip.io rows from the Prod desk IP until about 11-13 04:45Z.
**Your call:** The "< 20 restarts a day" bar under gr_lvzy0yxwgd counts merge-driven CI deploys, which the no-op guard can't lower: say whether to keep it as written (day 2 and 3 may miss it too) or judge that key result on "zero no-op restarts in three days" alone. (Proposal gr_ybymw15d4f is the plan that would look at the CI → deploy spacing itself.)

## Decided
- [dc_o6nmfoaenu](2026-11-06-gr-db6ofyd0yf-step-4-live-tick-median-73-ms-was-19-nmfoaenu.md) → approve (tick 73 ms live; grant closed by me)
- [dc_hljji3rohh](2026-11-06-gr-db6ofyd0yf-step-4-f7a22677-is-live-boot-05-06-4-jji3rohh.md) → approve (f7a22677 live, sampling parked 30 min)
- [dc_wkfc4gd3ay](2026-11-06-gr-q1jrelx2ty-step-3-confirmed-on-main-backup-rest-fc4gd3ay.md) → redirect (final step: merge PR #392 on green, claim kr_a4p4piyh7v, close; now held at the checkpoint)
- [dc_rw6hbqfe3z](2026-11-06-gr-ba0juhlm7n-day-check-11-05-11-06-clean-06-00z-c-6hbqfe3z.md) → approve (hourly backups day 11-05→11-06 clean; close waits on the drill)
- [dc_zek4m79opw](2026-11-06-gr-w9ue1k1p0c-day-4-of-7-clean-11-05-05-20z-11-06-k4m79opw.md) → approve (drain day 4 of 7 clean; resume-gap design note kept for the close)
- [dc_yy2psi1vd0](2026-11-06-gr-lvzy0yxwgd-day-1-read-14-restarts-since-the-gua-2psi1vd0.md) → approve (no-op day 1: 0 no-op restarts; day 2 parked to 11-07 04:30Z)
- [dc_z92lsjjzdl](2026-11-06-gr-8cdix9mpye-step-3a-live-ssrf-check-passes-on-mu-2lsjjzdl.md) → approve (SSRF guard live; Pages proof needs a PAT with repo-create rights)
- [dc_4sdkoccnmr](2026-11-06-grant-gr-db6ofyd0yf-adjusted-2-000-000-tokens-dkoccnmr.md), [dc_xaeg9mmvmi](2026-11-06-grant-gr-lvzy0yxwgd-adjusted-800-000-tokens-eg9mmvmi.md), [dc_9dvyd0hezy](2026-11-06-gr-db6ofyd0yf-step-3-pr-340-rebased-on-main-tests-vyd0hezy.md), [dc_xbiaxit5pr](2026-11-05-outbox-rule-noted-a-fly-org-token-in-the-town-hall-iaxit5pr.md), [dc_ho7hfbjs99](2026-11-05-outbox-cleanup-noted-dc-647d9m37u2-and-dc-y43rdv5z-7hfbjs99.md), [dc_ig0clc8awx](2026-11-06-grant-gr-8cdix9mpye-adjusted-1-500-000-tokens-0clc8awx.md), [dc_c11nq5dr2m](2026-11-06-grant-gr-w9ue1k1p0c-adjusted-1-000-000-tokens-1nq5dr2m.md), [dc_vvr35qv8ye](2026-11-06-grant-gr-q1jrelx2ty-adjusted-600-000-tokens-r35qv8ye.md) → approve (the four checkpoint continues/adjusts of 04:15–04:33Z and the step-3 confirmations they resumed)
- [dc_wewt9vcx6v](2026-11-06-mara-s-test-visitor-cl-test-visitor-ag-tgir6hsxv3-wt9vcx6v.md), [dc_j61644eaiw](2026-11-06-gr-q1jrelx2ty-step-3-minio-backup-restore-into-a-s-1644eaiw.md) → approve (gr_q1jrelx2ty step 3 PR #387 merged and confirmed on main)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_db6ofyd0yf (closed done) | kr_0cbw6jb2p8 live tick median < 110 ms | met (73 ms) | 970,844 / 2,000,000; 1,029,156 returned |
| gr_db6ofyd0yf | kr_50wtkdofgc bench p95 at 2× / 4× | met (152 ms / 400 ms) | |
| gr_db6ofyd0yf | kr_2djaq46ga6 cache-equivalence tests | met (CI green) | |
| gr_q1jrelx2ty (at checkpoint) | kr_nlbywt1hi4 CI restores a backup into a second town | claimed (main run 42166369737) | about 450,000 / 600,000 (the checkpoint card has the exact figure) |
| gr_q1jrelx2ty | kr_a4p4piyh7v docs path B pulls the image | on-track (PR #392, held) | |
| gr_lvzy0yxwgd | kr_s302el3vlj no-op redeploy doesn't restart | claimed (f318ec8) | about 400,000 / 800,000 |
| gr_lvzy0yxwgd | kr_vdql8siy01 tool text + FYI say CI deploys | claimed | |
| gr_lvzy0yxwgd | kr_u5n1x9hl00 3 days: no no-op restart, restarts24h < 20 | at-risk (day 1: 0 no-op, restarts24h 22) | |
| gr_w9ue1k1p0c | kr_245c17e700, kr_11595f1ae5 7 clean days | on-track (4 of 7) | about 490,000 / 1,000,000 |
| gr_w9ue1k1p0c | kr_9b2712691e cut team-lead session resumes | on-track, not yet seen live | |
| gr_8cdix9mpye | kr_7c07b8826c SSRF refusals live | claimed | about 420,000 / 1,500,000 |
| gr_8cdix9mpye | kr_dc79c27ff0, kr_89cb8eda84 (a real self-hosted town listed) | not-started, wait on the open outbox request | |
| gr_8cdix9mpye | kr_a7f8a181a6 register/verify curls | not-started | |
| gr_ba0juhlm7n | kr_y7u2m9hk9y, kr_cee8c26801 hourly verified backups | on-track (every run verified 11-05→11-06, lag peak 76 ms) | about 268,000 / 600,000 |
| gr_ba0juhlm7n | kr_bd08a0607a | claimed | |
| gr_ba0juhlm7n | kr_1a69c0a3be recovery drill row | not-started (drill in your in-tray) | |
| gr_z2v838adk9 (at checkpoint since #39) | unchanged | | 666k / 500k |

Spend today by lane: exploration 64,929 tokens (free under the goal 4,015,457); directed 0.

## Needs from Mitchell
- The directory's GitHub Pages proof (a stranger's Pages site registered and verified on muster.town) needs the test account's token to create a repo: the current MUSTER_TEST_GH_TOKEN is a fine-grained PAT that gets 403 on POST /user/repos. Either reissue it with Administration, Contents and Pages write on dungeonrpg99-ops, or say the fly.dev town you already have a request for is the only proof you want and Prod drops the Pages path.

_Already waiting in your in-tray: 2 proposals (gr_rcj8nkbkbt, gr_ybymw15d4f), 2 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 1 rollup ([dc_8why2czonj](2026-11-05-prod-rollup-40-checkpoint-gr-lvzy0yxwgd-227-760-20-hy2czonj.md))._
