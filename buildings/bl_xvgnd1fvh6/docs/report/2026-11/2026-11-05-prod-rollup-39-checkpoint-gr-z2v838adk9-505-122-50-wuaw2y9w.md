---
id: "dc_biwuaw2y9w"
type: "report"
state: "building"
title: "Prod rollup #39 (checkpoint gr_z2v838adk9, 505,122 / 500,000): a dead volume now restores itself from the newest good hourly copy and an empty town can't bury the backups, all live and tested; the timed 30-minute drill never ran because it needs flyctl on your machine"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_0z80k3w8hw","dc_zi69pv4wa8","dc_hexmsgulr1","dc_p44izut29y","dc_xx54hwjptq","dc_8b7yiroscr","dc_12t4j7s21n","dc_ti0zrakxk4","dc_c8snw9a8ig","dc_qdjp8md9mi","dc_v4uuak4qkh","dc_ven7cfjhqa","dc_h9d48ns3v5"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "pending"
sessionId: "se_9zykn8oq21"
assignmentId: "as_b2tz6mb18o"
costUsd: 3.2154107500000007
tokens: 160771
turns: 25
createdAt: "2026-11-05T02:45:05.086Z"
updatedAt: "2026-11-05T02:45:05.086Z"
---
Live: aa6f4fb since 2026-11-04 20:40 UTC (nothing new live since rollup #38). This is the second checkpoint report for the dead-volume recovery grant, which crossed its 500,000 tokens at 505,122. API and script changes only; no pictures.

## Shipped

**1. A dead volume comes back by itself from the newest good hourly copy, and a fresh empty town can never overwrite or bury the good backups**
**What it is:** Three pieces, all live since 11-01. First-boot restore: a server that boots with no town.db and the five backup values pulls the newest copy that decrypts and passes an integrity check, skipping a corrupt newer one. Empty-boot guard: a town with no backup history refuses to upload while the bucket holds copies, and no run ever replaces an object already there. One command, `deploy/recover.sh --yes`, does the whole recovery and refuses while muster.town still answers ok; a throwaway drill town boots with the runtime off so it never runs sessions or writes to the bucket (PRs #210 c1cdd23, #232 022946a, #239 7ca64bc).
**What you'd see:** `packages/server/test/backup.test.ts` on main: 27 tests green on main de42d38's CI run and again locally at 02:42Z today, including "a fresh town refuses to upload while the bucket holds copies" and "first boot restores the newest good copy, skipping a corrupt and a non-database newer one". GET https://muster.town/api/health at 02:41Z: backup.error null, lastAt = verifiedAt = 02:00:11Z, mode "hourly". `deploy/README.md` "Recover" (line 61) is the runbook; its Drill table (line 101) is still empty.
**Your call:** Continue with 40,000 more only if you will run the 25-minute recovery drill on your machine this week; otherwise Cut, since everything an agent can ship is live and only the timed proof is missing.

## Decided
- [dc_0z80k3w8hw](../2026-10/2026-10-31-gr-z2v838adk9-funded-repeat-its-three-steps-were-a-80k3w8hw.md) → approve (funded, steps queued)
- [dc_zi69pv4wa8](../2026-10/2026-10-31-gr-z2v838adk9-step-1-backup-guards-first-boot-rest-69pv4wa8.md) → approve (step 1 PR #210 parked on CI)
- [dc_hexmsgulr1](../2026-10/2026-10-31-prod-rollup-26-checkpoint-gr-z2v838adk9-dead-volum-xmsgulr1.md) → checkpoint #1 (rollup #26, continued to 500k)
- [dc_p44izut29y](2026-11-01-gr-z2v838adk9-step-1-pr-210-conflicted-with-227-s-4izut29y.md) → approve (PR #210 conflict with #227 resolved)
- [dc_xx54hwjptq](2026-11-01-gr-z2v838adk9-step-1-pr-210-merged-at-c1cdd23-park-54hwjptq.md) → approve (PR #210 merged c1cdd23)
- [dc_8b7yiroscr](2026-11-01-gr-z2v838adk9-step-1-verified-live-c1cdd23-s-first-7yiroscr.md) → approve (c1cdd23 verified live, 01:00Z run clean)
- [dc_12t4j7s21n](2026-11-01-gr-z2v838adk9-step-2-deploy-recover-sh-readme-reco-t4j7s21n.md) → approve (step 2 PR #232 parked on CI)
- [dc_ti0zrakxk4](2026-11-01-gr-z2v838adk9-step-2-pr-232-recover-sh-readme-reco-0zrakxk4.md) → approve (PR #232 merged 022946a)
- [dc_c8snw9a8ig](2026-11-01-gr-z2v838adk9-step-3-drill-request-in-the-outbox-d-snw9a8ig.md) → approve (drill request filed; parked)
- [dc_qdjp8md9mi](2026-11-02-recover-drill-dc-6gnk7y16y1-no-paste-back-yet-so-i-jp8md9mi.md) → approve (no paste-back 11-02, parked)
- [dc_v4uuak4qkh](2026-11-03-recover-drill-dc-6gnk7y16y1-still-no-paste-back-on-uuak4qkh.md) → approve (no paste-back 11-03, parked)
- [dc_ven7cfjhqa](2026-11-04-recover-drill-dc-6gnk7y16y1-still-no-paste-back-on-n7cfjhqa.md) → approve (no paste-back 11-04, parked)
- [dc_h9d48ns3v5](2026-11-05-recover-drill-dc-6gnk7y16y1-still-no-paste-back-on-d48ns3v5.md) → approve (no paste-back 11-05; final check scheduled 11-07 02:45Z, then the stop condition)

## Key results
gr_z2v838adk9 at checkpoint, 505,122 / 500,000. Of that, 108,182 tokens went to five sessions that waited for the drill paste-back (11-01 to 11-05).

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_17cd844e42 empty-boot guard | claimed | server test: bucket with town/…T20 object + fresh db → run() refuses, health backup.error set, object unchanged | backup.test.ts lines 320 and 537: run() returns null, health error "fresh town…", object bytes unchanged, nothing pruned; 27/27 green on main de42d38 and locally 02:42Z |
| kr_cc9dc81c96 first-boot restore picks newest good copy | claimed | test with fake S3: corrupt newest + good older → server starts with the good copy's agent count | backup.test.ts line 378 does exactly that, plus line 421 (seeds as before without env or a good copy); green |
| kr_36d053ac89 live unchanged after merge | claimed | health after the redeploy: backup.error null, lastAt == verifiedAt, < 70 min old | 11-01 01:00Z run clean after c1cdd23 ([dc_8b7yiroscr](2026-11-01-gr-z2v838adk9-step-1-verified-live-c1cdd23-s-first-7yiroscr.md)); 11-05 02:41Z: error null, lastAt = verifiedAt = 02:00:11Z, 41 min old |
| kr_7svvwv6lr5 back within 30 min of a new volume, no hand-built tarball | at-risk | README "Recover" records a timed drill ≤ 30 min with matching agent count and newest doc; guard tests green | Code and tests live; the Drill table is empty because the drill needs flyctl on a human's machine (asked 11-01, still open) |
| kr_ccca476c37 timed recovery drill | not-started | README "Recover": volume-created and health-ok ≤ 30 min apart, counts match the copy | Not run. Final check 11-07 02:45Z (sc_mdhwqbxb34); with nothing by then the grant's stop condition applies: steps 1-2 shipped, drill not run |

Other funded grants (unchanged since rollup #38): gr_ba0juhlm7n 227,428 / 600,000 (kr_bd08a0607a claimed; kr_y7u2m9hk9y, kr_cee8c26801 on-track, day 1 of hourly copies clean; kr_1a69c0a3be not-started); gr_w9ue1k1p0c 371,059 / 500,000 (all four not-started, days 1–2 of 7 clean); gr_8cdix9mpye 383,248 / 450,000 (not started). At checkpoint besides this one: gr_db6ofyd0yf 863,216 / 600,000 (rollup #36), gr_q1jrelx2ty 333,785 / 220,000 (rollup #37). Spend today: exploration 47,242 tokens, directed 0.

## Needs from Mitchell
- Continue (40,000 more) if you will run the 25-minute recovery drill on your machine this week: the command is already in your outbox, and the top-up fills the README Drill table from your paste-back and closes the grant. Cut if you won't: the restore, the guard and the one-command script are live and tested, and no amount of tokens can run the drill for you.

_Already waiting in your in-tray: 1 proposal (gr_lvzy0yxwgd), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), [dc_647d9m37u2](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md), [dc_y43rdv5zm7](../../../../../town-hall/outbox/2026-11/2026-11-01-hold-the-recover-drill-request-dc-647d9m37u2-until-3rdv5zm7.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 3 rollups ([dc_ezx0dndlg1](2026-11-04-prod-rollup-36-checkpoint-gr-db6ofyd0yf-601-494-60-x0dndlg1.md), [dc_ut9a8qxc9g](2026-11-04-prod-rollup-37-checkpoint-gr-q1jrelx2ty-225-544-22-9a8qxc9g.md), [dc_ckxutpcciq](2026-11-05-prod-rollup-38-hourly-off-site-backup-now-holds-th-xutpcciq.md))._
