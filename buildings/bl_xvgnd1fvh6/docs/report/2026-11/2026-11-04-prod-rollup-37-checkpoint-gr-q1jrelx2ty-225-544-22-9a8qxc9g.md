---
id: "dc_ut9a8qxc9g"
type: "report"
state: "building"
title: "Prod rollup #37 (checkpoint gr_q1jrelx2ty, 225,544 / 220,000): a public Docker image of the town is built and smoke-tested by CI on every green main; backup/restore in CI and the pull-and-run docs page are not started, 100k more finishes both"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_jqrsoj7l1j","dc_acoggjhacn","dc_k80n4lc4p1","dc_ukieylf211","dc_syrgtz34p7","dc_arw76kawkw"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/310","https://github.com/mitchellgordon95/agent-town/pull/342","https://github.com/mitchellgordon95/agent-town/actions/runs/41899336530"]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "pending"
sessionId: "se_bgwaj39955"
assignmentId: "as_6fo8ufmoqc"
costUsd: 2.1648215000000004
tokens: 108241
turns: 20
createdAt: "2026-11-04T19:52:18.965Z"
updatedAt: "2026-11-04T19:52:18.965Z"
---
Live: 4815e19 since 2026-11-04 19:33 UTC. This is the checkpoint report for the self-host image grant, which crossed its 220,000 tokens at 225,544. Two of its four key results are claimed, two are not started. Nothing in this grant touches muster.town itself: both PRs changed only `.github/`, so CI did not redeploy for them.

## Shipped

**1. Anyone can pull a ready-made Docker image of the town, with no login**
**What it is:** CI now builds the server image off Fly with a plain `docker build` on every green main and pushes it to GitHub's registry as `ghcr.io/mitchellgordon95/muster-town:prod` and `:<sha>`. The package is public (537 MB, amd64) and took 81–83 s per build. PR #310, report [dc_ukieylf211](2026-11-04-gr-q1jrelx2ty-step-1-done-ci-pushes-a-public-ghcr-ieylf211.md).
**What you'd see:** `docker pull ghcr.io/mitchellgordon95/muster-town:prod` works on any machine without a GitHub login. Checked anonymously from a desk at 19:50 UTC: 12 tags listed, and `:prod` has the same digest as `:17d00eb`, which is the head of the prod branch. The live server is still at 4815e19 (promote restarts at most every 15 min), and that commit has no tag because the merge storm cancelled its run. No picture: registry and CI only.
**Your call:** None.

**2. Every image is boot-tested the way the self-host page says, before it is pushed**
**What it is:** The image job now runs the self-host page's path B compose on the CI runner against the just-built image: a fresh town, health ok with the right commit, the admin token works, `docker compose restart`, and the same checks again. The push happens only if that passes. It also runs on PRs without pushing. PR #342, report [dc_arw76kawkw](2026-11-04-gr-q1jrelx2ty-step-2-done-path-b-compose-smoke-run-w76kawkw.md).
**What you'd see:** On GitHub Actions, main run 41899336530 (head 17d00eb) has a green step "image smoke (self-host path B)" from 19:45:35 to 19:46:05 UTC, with health ok before and after the restart, then the push at 19:46:40 UTC. The whole image job takes about 1 min 47 s. Caveat: runs on main after 17d00eb show "cancelled" because merges landed every 1–2 min; PR #338 makes them queue instead. No picture: CI only.
**Your call:** None.

## Decided
- [dc_acoggjhacn](2026-11-04-gr-q1jrelx2ty-funded-220k-cut-into-4-steps-one-per-oggjhacn.md) → approve (plan: 4 steps, one per key result)
- [dc_jqrsoj7l1j](2026-11-04-gr-q1jrelx2ty-step-1-ci-image-job-in-pr-310-parked-rsoj7l1j.md) → approve (PR #310 opened, parked on CI)
- [dc_k80n4lc4p1](2026-11-04-gr-q1jrelx2ty-step-1-pr-310-merged-as-04160f9-park-0n4lc4p1.md) → approve (PR #310 merged as 04160f9)
- [dc_ukieylf211](2026-11-04-gr-q1jrelx2ty-step-1-done-ci-pushes-a-public-ghcr-ieylf211.md) → continue (step 1 verified; step 2 assigned)
- [dc_syrgtz34p7](2026-11-04-gr-q1jrelx2ty-step-2-path-b-compose-smoke-in-the-i-rgtz34p7.md) → approve (PR #342 opened, parked on CI)
- [dc_arw76kawkw](2026-11-04-gr-q1jrelx2ty-step-2-done-path-b-compose-smoke-run-w76kawkw.md) → continue (step 2 verified; step 3 queued, now held at the checkpoint)

## Key results
This grant, gr_q1jrelx2ty, 225,544 / 220,000:

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_gec7ivzfxs public image `:prod` + `:<sha>` pushed on every green main | claimed | anonymous `docker pull …:prod`; package tag equals the prod sha | tags/list 200 with 12 tags at 19:50 UTC; `:prod` = `:17d00eb` = origin/prod (sha256:8ca7fbfc…f17c); live 4815e19 untagged (run cancelled) |
| kr_emrv9hzs47 CI boots the image per path B, survives a restart | claimed | latest main run has a green "image smoke" step, health ok before and after restart | run 41899336530: green, 19:45:35→19:46:05 UTC; later main runs cancelled by the merge storm |
| kr_nlbywt1hi4 hourly backup to S3 and restore into a second container in CI | not-started | green "image backup/restore" step with backup.verifiedAt and equal agent counts | no PR yet; plan ready as as_etspipc4fa (MinIO service, ~60k) |
| kr_a4p4piyh7v docs path B pull-and-run, gaps #1 and #8 struck | not-started | docs/self-host.md path B uses the ghcr image; #1 and #8 struck | path B still `image: muster-town:local` with build steps; only #2 and #7 struck |

Other funded grants:

| Grant | Key results | Spent / granted |
|---|---|---|
| gr_ba0juhlm7n hourly backups | kr_y7u2m9hk9y on-track, kr_bd08a0607a claimed, kr_cee8c26801 on-track, kr_1a69c0a3be not-started | 227,428 / 600,000 |
| gr_z2v838adk9 one-command recovery | kr_7svvwv6lr5 at-risk, kr_17cd844e42 on-track, kr_cc9dc81c96 on-track, kr_36d053ac89 not-started, kr_ccca476c37 not-started | 487,503 / 500,000 |
| gr_w9ue1k1p0c redeploys keep sessions | kr_ohom5phapo, kr_245c17e700, kr_11595f1ae5, kr_9b2712691e all not-started (days 1–2 of 7 clean) | 371,059 / 500,000 |
| gr_8cdix9mpye directory registration | kr_og03nxrkct, kr_a7f8a181a6, kr_dc79c27ff0, kr_7c07b8826c, kr_89cb8eda84 not-started | 383,248 / 450,000 |
| gr_db6ofyd0yf runtime tick (at checkpoint, rollup #36) | kr_0cbw6jb2p8 at-risk, kr_50wtkdofgc on-track, kr_2djaq46ga6 claimed | 863,216 / 600,000 |

Spend today by lane: exploration 95,371 tokens (free under the goal: 398,516), directed 198,085 tokens.

## Needs from Mitchell
- Continue this grant with the 100,000-token top-up, adjust it, or cut it. A continue finishes the two open key results: a backup to MinIO and a restore into a second container inside the same CI smoke (~60k), then the self-host page's path B rewritten to pull-and-run from the ghcr image with gaps #1 and #8 struck (~25k). A cut leaves a public, boot-tested image but a docs page that still tells strangers to build it themselves.

_Already waiting in your in-tray: 1 proposal (gr_lvzy0yxwgd), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), [dc_647d9m37u2](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md), [dc_y43rdv5zm7](../../../../../town-hall/outbox/2026-11/2026-11-01-hold-the-recover-drill-request-dc-647d9m37u2-until-3rdv5zm7.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 1 rollup ([dc_ezx0dndlg1](2026-11-04-prod-rollup-36-checkpoint-gr-db6ofyd0yf-601-494-60-x0dndlg1.md))._
