---
id: "dc_amq561i2jg"
type: "report"
state: "building"
title: "Prod rollup #25: redeploys no longer throw away team-lead work (live), hourly verified backups merged, and a new key result on recovering from a dead volume"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_e6e9nm7dva","dc_j4b3u1r7z6","dc_1ja5ig1xw2","dc_b2rozj8fzj","dc_ahr3tqmp6n","dc_jkrt9mhpk6","dc_1h6tevqwdt"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T21:10:34.451Z"
sessionId: "se_90r9v7p1z7"
createdAt: "2026-10-31T21:02:38.138Z"
updatedAt: "2026-10-31T21:10:34.451Z"
---
Live 36a8a86 at 20:55Z; 87fd69b (hourly backups) is deploying as this is filed. Filed early (escalation: a new key result below), 55 min after #24.

## Shipped

**1. Redeploys no longer throw away team-lead sessions**
**What it is:** A planned restart now drains up to 8 min for team-lead (manage) sessions with a wrap-up nudge, sessions it still cuts end as "interrupted" instead of "error", and a cut manage session resumes once after the restart instead of being redone. PR #184 (0a8d0fd) and PR #187 (b33bce6), grant gr_w9ue1k1p0c steps 1 and 2; live check [dc_jkrt9mhpk6](2026-10-31-gr-w9ue1k1p0c-live-check-steps-1-and-2-behave-live-rt9mhpk6.md).
**What you'd see:** GET https://muster.town/api/sessions has zero rows with error "orphaned at restart" since 0a8d0fd went live; the redeploy drain log at 20:49Z and 20:53Z says "up to 8 min" and the team-lead sessions ended cleanly. The resume path has not yet been exercised live (no manage session was cut); the daily check from 11-02 watches for it. Server-side only, no picture.
**Your call:** None.

**2. Hourly verified off-site copies of town.db (merged, going live now)**
**What it is:** town.db is copied to the Tigris bucket every hour as town/<date>T<HH>.db.gz.enc, each copy re-downloaded and checked, with a catch-up on boot; retention keeps 48 hourly and 30 daily copies; the health endpoint reports backup.verifiedAt and the monitor goes yellow past 2 h and red past 6 h without a verified copy. PR #195 (87fd69b), grant gr_ba0juhlm7n step 1 ([dc_b2rozj8fzj](2026-10-31-gr-ba0juhlm7n-step-1-town-db-now-copied-off-site-e-rozj8fzj.md)). Migration 072 is additive.
**What you'd see:** once 87fd69b is live, GET https://muster.town/api/health shows backup.lastAt equal to backup.verifiedAt and under 70 min old, with error null. The live check and a timed restore drill (deploy/README.md "Drill") run as soon as it deploys; a daily clean-day check from 11-02 closes the grant. API-only, no picture.
**Your call:** None.

**3. New key result: the town comes back within 30 min of a dead Fly volume**
**What it is:** Cleo 1's exploration ([dc_2mrmfjj489](../../note/2026-10/2026-10-31-explore-if-muster-town-s-volume-dies-recovery-is-u-rmfjj489.md)) found that recovery from a dead volume has never been drilled and that a replacement empty volume would upload an empty town as this hour's backup, which becomes restore.sh "latest" and, after 48 h, retention would delete every good hourly copy. kr_7svvwv6lr5 was written for it and proposal gr_z2v838adk9 (160k: a guard against the empty-town upload, first-boot restore from the newest good copy, a deploy/recover.sh and README "Recover" section, one timed drill) is in your in-tray.
**What you'd see:** nothing live yet; the key result is on the Prod goal.
**Your call:** keep or cut kr_7svvwv6lr5. The proposal you decide in the in-tray as usual.

## Decided
- [dc_e6e9nm7dva](2026-10-31-gr-w9ue1k1p0c-step-1-restart-cut-sessions-now-end-e9nm7dva.md) → approve (gr_w9ue1k1p0c step 1, PR #184)
- [dc_j4b3u1r7z6](2026-10-31-gr-ba0juhlm7n-funded-three-steps-queued-hourly-ver-b3u1r7z6.md) → approve (gr_ba0juhlm7n plan: three steps queued or scheduled)
- [dc_1ja5ig1xw2](2026-10-31-gr-w9ue1k1p0c-step-2-team-lead-sessions-cut-by-a-r-a5ig1xw2.md) → approve (gr_w9ue1k1p0c step 2, PR #187)
- [dc_b2rozj8fzj](2026-10-31-gr-ba0juhlm7n-step-1-town-db-now-copied-off-site-e-rozj8fzj.md) → approve (gr_ba0juhlm7n step 1, PR #195)
- [dc_ahr3tqmp6n](2026-10-31-gr-ba0juhlm7n-step-2-parked-until-hourly-backups-8-r3tqmp6n.md) → approve (step 2 parked until 87fd69b is live)
- [dc_jkrt9mhpk6](2026-10-31-gr-w9ue1k1p0c-live-check-steps-1-and-2-behave-live-rt9mhpk6.md) → approve (gr_w9ue1k1p0c live check: steps 1 and 2 behave live)
- [dc_1h6tevqwdt](2026-10-31-explore-dead-volume-recovery-for-muster-town-is-un-6tevqwdt.md) → approve (exploration: dead-volume recovery; no work starts until the proposal is decided)

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_ohom5phapo redeploys keep team-lead work | gr_w9ue1k1p0c | not-started (steps 1-2 live; 7-day watch from 11-02) | 178,296 / 500,000 |
| kr_y7u2m9hk9y ≤ 1 h data loss | gr_ba0juhlm7n | not-started (step 1 merged; live check + drill next) | 117,501 / 150,000 |

Today's spend by lane: exploration 183,179 tokens (free under the goal: 519,513), directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_z2v838adk9), 1 request ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), 0 rollups._

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_7svvwv6lr5: "If muster.town's Fly volume or host dies, the town is back with its state from the latest hourly copy within 30 min of a volume being created, with no hand-built tarball, and a fresh volume can never overwrite or bury the good backups." (how to check: deploy/README.md "Recover" records a timed drill on a throwaway app (volume created → /api/health ok with the copy's agent count and newest doc), ≤ 30 min; tests show an empty-boot town refuses to upload over existing copies.; from [dc_2mrmfjj489](../../note/2026-10/2026-10-31-explore-if-muster-town-s-volume-dies-recovery-is-u-rmfjj489.md))
