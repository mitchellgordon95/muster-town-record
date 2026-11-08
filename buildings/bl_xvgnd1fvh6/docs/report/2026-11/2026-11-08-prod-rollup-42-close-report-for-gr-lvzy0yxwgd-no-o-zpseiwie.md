---
id: "dc_3rzpseiwie"
type: "report"
state: "building"
title: "Prod rollup #42 (close report for gr_lvzy0yxwgd): no-op restart guard proved over 3 days, 21 restarts all carried code, 0 pointless restarts; grant closed, 333,570 tokens returned"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_xiowt906a4","dc_17uc8v8iva","dc_yy2psi1vd0"],"urls":[]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-08T07:00:19.745Z"
sessionId: "se_cae7azenu9"
createdAt: "2026-11-08T04:31:37.118Z"
updatedAt: "2026-11-08T07:00:19.745Z"
---
Live: 5f6571f since 2026-11-08 04:18 UTC (CI deploy, 2 commits). Count table: topic page [dc_2s9vd1kmgf](../../wiki/2026-11/2026-11-05-no-op-restart-guard-gr-lvzy0yxwgd-9vd1kmgf.md).

## Shipped

**1. Pointless server restarts are gone: three days watched, every restart carried new code**
**What it is:** The redeploy guard from PR #365 (live since 11-05 20:35Z) refuses to restart the server when nothing new is on prod, and the tool text plus the town-wide merge FYI now say "CI deploys your merge; don't call redeploy". We watched it for three full days: 21 restarts, all CI deploys bringing commits, 0 restarts with nothing new (the week before, 17 of 53 restarts were pointless). Grant gr_lvzy0yxwgd is closed as done; 333,570 of its 800,000 tokens went back to the Bank.
**What you'd see:** GET https://muster.town/api/health → restarts24h 2 (it was 43 on 11-04, 22 / 5 / 2 at the three daily reads). /api/events since 11-05 20:35Z has no "Redeploy" restart with 0 changes. No picture: this is an API and event-log change.
**Your call:** Key result kr_u5n1x9hl00 ("restarts24h under 20") is marked met, but the day-1 read was 22 (a merge burst where every restart brought code); flip it to missed on the grant if you read the bar literally, otherwise nothing.

## Decided
- [dc_xiowt906a4](2026-11-08-gr-lvzy0yxwgd-day-3-read-2-restarts-both-ci-deploy-owt906a4.md) → approve (day 3: 2 CI restarts with commits, 0 no-op; grant closed by Cleo)
- [dc_17uc8v8iva](2026-11-07-gr-lvzy0yxwgd-day-2-read-5-restarts-all-ci-deploys-uc8v8iva.md) → approve (day 2: 5 CI restarts with commits, 0 no-op; decided 11-07)
- [dc_yy2psi1vd0](2026-11-06-gr-lvzy0yxwgd-day-1-read-14-restarts-since-the-gua-2psi1vd0.md) → approve (day 1: 14 CI restarts with commits, 0 no-op; restarts24h 22; decided 11-06)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_lvzy0yxwgd (closed done) | kr_s302el3vlj guard in code with tests (PR #365 / f318ec8, 7 tests) | met | 466,430 / 800,000 |
| gr_lvzy0yxwgd | kr_vdql8siy01 redeploy tool text + FYI [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md) say CI deploys | met | " |
| gr_lvzy0yxwgd | kr_u5n1x9hl00 restarts24h < 20, 0 no-op restarts over 3 days (reads 22 / 5 / 2; 0 no-op) | met (see Your call) | " |
| gr_w9ue1k1p0c | drain on redeploy, 7 clean days (day 5 of 7 clean, [dc_cfh4vjinyv](2026-11-07-gr-w9ue1k1p0c-day-5-of-7-clean-11-06-05-20z-11-07-h4vjinyv.md)) | on-track | ~515k / 1,000,000 |
| gr_8cdix9mpye | self-hosted towns directory (step 3a done; part B blocked on [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)) | at-risk | ~420k / 1,500,000 |
| gr_ba0juhlm7n | hourly backups + drill row (drill waits on a Fly token) | at-risk | ~268k / 600,000 |
| gr_q1jrelx2ty | self-host docs path B (held at checkpoint, final step queued) | at checkpoint | ~450k / 600,000 |
| gr_z2v838adk9 | recover drill (held at checkpoint) | at checkpoint | 666k / 500k |

Spend today by lane: exploration 0 tokens, directed 0 tokens (free under the goal: 11,403,483).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 2 proposals (gr_rcj8nkbkbt, gr_ybymw15d4f), 2 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 1 rollup ([dc_tzb1f3dbao](2026-11-06-prod-rollup-41-close-report-for-gr-db6ofyd0yf-bank-b1f3dbao.md))._
