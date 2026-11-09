---
id: "dc_bpkmunmsjc"
type: "report"
state: "building"
title: "Prod rollup #44 (close report for gr_q1jrelx2ty, 513,006 / 800,000): a stranger can run their own Muster Town from the published image; CI proves the image boots and restores a backup on every green main"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_316drno42y","dc_wkfc4gd3ay","dc_3z8ch8kfwp","dc_mfzesq3d8w","dc_j61644eaiw","dc_ut9a8qxc9g"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/392","https://github.com/mitchellgordon95/muster-town/pull/310","https://github.com/mitchellgordon95/muster-town/pull/342","https://github.com/mitchellgordon95/muster-town/pull/387"]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-09T22:35:23.592Z"
sessionId: "se_d584p7hdk1"
createdAt: "2026-11-09T22:35:23.504Z"
updatedAt: "2026-11-09T22:35:23.592Z"
---
Live: 4773902 (since 18:52 UTC today). PR #392 (docs only, b9a248b0) merged at 22:33 UTC and moves prod without a restart.

## Shipped

**1. A stranger runs their own Muster Town from a published image, and CI proves it works on every green main**
**What it is:** The self-host grant is done and closed. CI publishes a public Docker image of every green main (ghcr.io/mitchellgordon95/muster-town:prod, plus a :sha tag per commit), boots the self-host path-B compose from that image and checks health before and after a restart, and restores a backup into a fresh town. docs/self-host.md path B now points at the image: no clone, no build. Closed as done at 513,006 of the 800,000 you adjusted it to 2 minutes before; 286,994 tokens returned to the Bank. Four key results met (gr_q1jrelx2ty, close doc [dc_ut9a8qxc9g](2026-11-04-prod-rollup-37-checkpoint-gr-q1jrelx2ty-225-544-22-9a8qxc9g.md); PRs #310, #342, #387, #392).
**What you'd see:** On any machine with Docker, `docker pull ghcr.io/mitchellgordon95/muster-town:prod` works anonymously; at 22:3x UTC `:prod` and `:4773902d…` share digest sha256:37641883…, the commit /api/health reports. docs/self-host.md path B line 119 reads `image: ghcr.io/mitchellgordon95/muster-town:prod`, gaps #1 and #8 struck through. CI main run 42166369737 shows `image smoke (self-host path B)` green and `[restore] … ok, 3 agents`. A CI and docs change: no picture.
**Your call:** None. The grant is closed; flip a key result to missed on the grant if you disagree with any of the four.

## Decided
- [dc_316drno42y](2026-11-09-gr-q1jrelx2ty-step-4-done-pr-392-merged-b9a248b0-s-6drno42y.md) → approve (step 4: PR #392 merged b9a248b0; close_grant gr_q1jrelx2ty run by me: done, 4 KRs met)
- [dc_wkfc4gd3ay](2026-11-06-gr-q1jrelx2ty-step-3-confirmed-on-main-backup-rest-fc4gd3ay.md), [dc_3z8ch8kfwp](2026-11-06-gr-q1jrelx2ty-step-3-pr-387-green-backup-to-s3-res-8ch8kfwp.md), [dc_mfzesq3d8w](2026-11-06-gr-q1jrelx2ty-step-3-iteration-2-minio-minio-is-go-zesq3d8w.md), [dc_j61644eaiw](2026-11-06-gr-q1jrelx2ty-step-3-minio-backup-restore-into-a-s-1644eaiw.md) → approved earlier (steps 1–3 and the hold; folded here as the close record)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_q1jrelx2ty (closed, done) | kr_gec7ivzfxs: public image per green main | met | 513,006 / 800,000 (286,994 returned) |
| gr_q1jrelx2ty | kr_emrv9hzs47: CI boots path B from the image | met | |
| gr_q1jrelx2ty | kr_nlbywt1hi4: CI restores a backup into a fresh town | met | |
| gr_q1jrelx2ty | kr_a4p4piyh7v: docs path B uses the image, no clone or build | met | |
| gr_8cdix9mpye (funded) | kr_dc79c27ff0, kr_89cb8eda84: directory registration from a real self-hosted town | waiting on outbox [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md) | ~420,000 / 1,500,000 |
| gr_8cdix9mpye | other key results | step 3a done (SSRF guard live), 3b waits on the same request | |
| gr_ba0juhlm7n (funded) | hourly off-site backups, restore drill row | backups live; drill row empty, waits on outbox [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) | ~268,000 / 600,000 |
| gr_z2v838adk9 (cut by you 22:31 UTC) | 3 claimed, 1 at-risk, 1 not started | cut | 665,893 / 500,000 |

Spend today by lane: exploration 0, directed 0; grant lane: this close (step 4) ~39,000.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 2 proposals (gr_rcj8nkbkbt, gr_ybymw15d4f), 2 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 2 rollups ([dc_tzb1f3dbao](2026-11-06-prod-rollup-41-close-report-for-gr-db6ofyd0yf-bank-b1f3dbao.md), [dc_cges6f5hvy](2026-11-09-prod-rollup-43-close-report-for-gr-w9ue1k1p0c-rede-es6f5hvy.md))._
