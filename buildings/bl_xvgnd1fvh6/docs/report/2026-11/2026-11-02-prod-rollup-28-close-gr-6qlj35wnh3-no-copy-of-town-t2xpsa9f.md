---
id: "dc_42t2xpsa9f"
type: "report"
state: "building"
title: "Prod rollup #28 (close gr_6qlj35wnh3): no copy of town.db hands over a credential any more; the hourly export runs off the main thread; a restore drill town spends nothing"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_st21vw4l9n","dc_99pq8kvsgo","dc_8kz3scjc33","dc_3f73o1f8aj","dc_b3vrlbhbd5","dc_qdjp8md9mi","dc_2ns1jgf0fu","dc_cgdu740k3s","dc_5tel7zzvdk","dc_zbb8byig63","dc_w0mppbg8tr","dc_w1l2a32d2c","dc_s2jnkra5fp","dc_22fwety8n1"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-02T03:02:15.362Z"
sessionId: "se_2c5irxk8k9"
createdAt: "2026-11-02T02:27:59.498Z"
updatedAt: "2026-11-02T03:02:15.362Z"
---
Live dab5b9b since 2026-11-02 02:24 UTC; it contains every commit below. This rollup closes grant gr_6qlj35wnh3 as done (368,334 of 400,000 tokens; 31,666 returned). The three RED "sessions" FYIs on the Prod board since 11-01 21:24 UTC were claude-fable-5-1 sessions hitting the Fable monthly spend limit, not tokens and not deploys; all cleared, and Pix's dab5b9b addresses the Bank side.

## Shipped
**1. The Bank's credentials and every login token are encrypted or hashed at rest, and nobody got logged out**
**What it is:** Two PRs. #246 (244d9d1) stores the subscription token and API keys in the Bank as ciphertext and decrypts them only inside the one chooser every session goes through; a copy of town.db no longer carries a usable Claude credential. #251 (c50aa8c, migration 079) stores login tokens as sha256 in place with an idempotent boot back-fill, and gives each desk and host session its own token that is revoked when the session ends. Reports [dc_s2jnkra5fp](2026-11-01-gr-6qlj35wnh3-step-2-live-bank-secrets-encrypted-a-jnkra5fp.md), [dc_b3vrlbhbd5](2026-11-01-gr-6qlj35wnh3-step-3-live-login-tokens-hashed-c50a-vrlbhbd5.md); docs/secrets.md "Login tokens".
**What you'd see:** API-only change, no picture. After the 11-01 22:02 UTC deploy two desks that started on old plaintext tokens finished `done`, new sessions run on per-session tokens, /api/sessions has no error rows after it, health ok with backup.error null. Your browser sign-in uses a signed cookie, so it was untouched. Copies taken before 11-01 still hold plaintext until retention removes them (30 daily copies).
**Your call:** None.

**2. The hourly export runs in a worker: exactly one export per hour, main thread no longer stalled**
**What it is:** 503 follow-up B2, PR #235 (9484ad6): the hourly export moved to a worker thread and the double append is gone. Reports [dc_2ns1jgf0fu](2026-11-01-kr-1a69c0a3be-02-00z-backup-run-held-lagms-at-109-s1jgf0fu.md), [dc_8kz3scjc33](2026-11-01-503-follow-up-b2-live-exactly-one-export-done-per-z3scjc33.md).
**What you'd see:** API-only change, no picture. /api/events over 11-01 02:29 to 21:23 UTC: 18 export.done events, one per hour at boot + n h + ~5 s, files 2,044 to 2,047. Desk measurement: main-thread max gap 17 to 18 ms through the worker against 2.1 to 3.2 s before; no lag FYI on the board that day. A direct live lag sample across one export is queued for the ~03:24 UTC run (as_733d1qu347). Every export.done still has commit null: git on Fly fails (exploration as_4y4e3g8vs4, held for free tokens).
**Your call:** None.

**3. Throwaway mode: a restore or recover drill town spends no Claude tokens and writes nothing to the backup bucket**
**What it is:** PR #239 (7ca64bc): MUSTER_TOWN_THROWAWAY turns the runtime and the backup off and logs "[server] runtime off (throwaway)"; deploy/recover.sh and restore.sh set it. Report [dc_cgdu740k3s](2026-11-01-gr-6qlj35wnh3-funded-step-1-throwaway-mode-is-alre-du740k3s.md).
**What you'd see:** Nothing on muster.town; it shows in the drill log of the next recover drill. API-only change, no picture.
**Your call:** The Recover drill waiting in the outbox ([dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)) is now the only thing between gr_z2v838adk9 and its close, and it also proves this key result; when you run it, paste the log back there.

## Decided
- [dc_2ns1jgf0fu](2026-11-01-kr-1a69c0a3be-02-00z-backup-run-held-lagms-at-109-s1jgf0fu.md) (export worker lag evidence) → approve
- [dc_cgdu740k3s](2026-11-01-gr-6qlj35wnh3-funded-step-1-throwaway-mode-is-alre-du740k3s.md) (throwaway mode PR #239) → approve
- [dc_5tel7zzvdk](2026-11-01-gr-6qlj35wnh3-step-2-bank-secrets-encrypted-at-res-el7zzvdk.md) → approve
- [dc_zbb8byig63](2026-11-01-explore-no-written-path-to-scale-past-muster-town-b8byig63.md) (scale-path finding; proposal gr_n0p3ast5pp) → approve
- [dc_w0mppbg8tr](2026-11-01-gr-6qlj35wnh3-step-2-pr-246-merged-as-244d9d1-park-mppbg8tr.md) → approve
- [dc_w1l2a32d2c](2026-11-01-retainers-both-prod-schedules-sized-at-30-000-toke-l2a32d2c.md) → approve
- [dc_s2jnkra5fp](2026-11-01-gr-6qlj35wnh3-step-2-live-bank-secrets-encrypted-a-jnkra5fp.md) (Bank secrets encrypted, live) → approve
- [dc_22fwety8n1](2026-11-01-retainer-asks-filed-sc-ul1b1ntqik-240k-8-30k-and-s-fwety8n1.md) (retainer asks filed) → approve
- [dc_st21vw4l9n](2026-11-01-gr-6qlj35wnh3-step-3-login-tokens-hashed-per-sessi-21vw4l9n.md) (PR #251 open) → approve
- [dc_99pq8kvsgo](2026-11-01-gr-6qlj35wnh3-step-3-pr-251-ci-failed-on-main-s-de-pq8kvsgo.md) (PR #251 CI: main's deadcode bug) → approve
- [dc_3f73o1f8aj](2026-11-01-gr-6qlj35wnh3-step-3-pr-251-merged-as-c50aa8c-park-73o1f8aj.md) (PR #251 merged c50aa8c) → approve
- [dc_b3vrlbhbd5](2026-11-01-gr-6qlj35wnh3-step-3-live-login-tokens-hashed-c50a-vrlbhbd5.md) (login tokens hashed, live) → approve
- [dc_qdjp8md9mi](2026-11-02-recover-drill-dc-6gnk7y16y1-no-paste-back-yet-so-i-jp8md9mi.md) (drill: no paste-back, parked to 11-03) → approve
- [dc_8kz3scjc33](2026-11-01-503-follow-up-b2-live-exactly-one-export-done-per-z3scjc33.md) (export cadence proven, lag sample owed) → redirect: as_733d1qu347, direct lag sample across the next export (directed, 1:1 mt_rakiuxsb7w)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_6qlj35wnh3 (closed done) | kr_fbmcxyzot1 Bank secrets encrypted, sessions still run | claimed | 368,334 / 400,000 |
| gr_6qlj35wnh3 | kr_9qpk2gnwa9 login tokens hashed, no forced logout | claimed | |
| gr_6qlj35wnh3 | kr_zz0nm8ets4 drill town spends nothing (mark once the drill log is in) | claimed | |
| gr_ba0juhlm7n hourly backups | kr_y7u2m9hk9y ≤ 1 h loss | on-track | 227,428 / 600,000 |
| gr_ba0juhlm7n | kr_bd08a0607a unit tests | claimed | |
| gr_ba0juhlm7n | kr_cee8c26801 live cadence for a day (retainer sc_zyj6w0mygq, awaiting approval) | on-track | |
| gr_ba0juhlm7n | kr_1a69c0a3be live cost (lag 109 ms max, [dc_2ns1jgf0fu](2026-11-01-kr-1a69c0a3be-02-00z-backup-run-held-lagms-at-109-s1jgf0fu.md)) | not-started | |
| gr_z2v838adk9 dead-volume recovery | kr_7svvwv6lr5 30-min recovery | at-risk | 452,541 / 500,000 |
| gr_z2v838adk9 | kr_17cd844e42 empty-boot guard | on-track | |
| gr_z2v838adk9 | kr_cc9dc81c96 first-boot restore skips a corrupt copy | on-track | |
| gr_z2v838adk9 | kr_36d053ac89 live unchanged after merge | not-started | |
| gr_z2v838adk9 | kr_ccca476c37 timed drill (waits on [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)) | not-started | |
| gr_w9ue1k1p0c redeploys keep sessions | kr_ohom5phapo, kr_245c17e700, kr_11595f1ae5, kr_9b2712691e (daily check = retainer sc_ul1b1ntqik, awaiting approval) | not-started | 371,059 / 500,000 |
| gr_8cdix9mpye directory | kr_og03nxrkct, kr_a7f8a181a6, kr_dc79c27ff0, kr_7c07b8826c, kr_89cb8eda84 | not-started | 383,248 / 450,000 |

Today's spend by lane: exploration 0 tokens (free under the goal: 0), directed 0 tokens. Two exploration assignments (export git failure, morning check) are held because no tokens are free under the goal.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_n0p3ast5pp), 5 requests ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md), [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md), [dc_647d9m37u2](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-7d9m37u2.md), [dc_y43rdv5zm7](../../../../../town-hall/outbox/2026-11/2026-11-01-hold-the-recover-drill-request-dc-647d9m37u2-until-3rdv5zm7.md), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), 0 rollups._
