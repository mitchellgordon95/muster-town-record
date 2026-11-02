---
id: "dc_3nt83elkjl"
type: "report"
state: "building"
title: "Prod rollup #27 (checkpoint gr_ba0juhlm7n): hourly verified backups are live and landing, unit tests claimed; over budget by ~7k because the incident cut a step mid-run; asking ~65k to finish the drill and the day of checks"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_j4b3u1r7z6","dc_b2rozj8fzj","dc_ahr3tqmp6n"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-01T00:47:03.353Z"
sessionId: "se_1dwcv348c1"
assignmentId: "as_xusuohvc0n"
costUsd: 2.0164619999999998
tokens: 40329
turns: 21
createdAt: "2026-10-31T22:22:42.213Z"
updatedAt: "2026-11-01T00:47:03.353Z"
---
Live ae18eb3 (health at 22:20:06Z: backup lastAt == verifiedAt == 2026-10-31T22:00:11Z, 33,285,099 bytes, error null, monitor alerts [], lag 74 ms). This is the 100% checkpoint for gr_ba0juhlm7n (hourly encrypted off-site copies of town.db), 152,893 / 150,000 tokens at the crossing, about 157,000 now.

## Shipped
**1. town.db is copied off-site every hour and each copy is checked by downloading it back**
**What it is:** PR #195 (https://github.com/mitchellgordon95/muster-town/pull/195, merged as 87fd69b, in the live build). Every hour on the hour the server copies town.db, encrypts it, uploads it to the Tigris bucket as town/<date>T<HH>.db.gz.enc, then downloads it again, decrypts it and runs an integrity check before counting the run. Retention keeps the newest 48 hourly copies plus one per day for 30 days. A boot catch-up runs if the last copy is over an hour old. Worst-case loss from a dead volume drops from about 24 h to about 1 h once a restore from an hourly copy is proven (owed, see Key results). Report [dc_b2rozj8fzj](2026-10-31-gr-ba0juhlm7n-step-1-town-db-now-copied-off-site-e-rozj8fzj.md).
**What you'd see:** GET https://muster.town/api/health → backup: lastAt and verifiedAt equal and under 70 min old, error null. Two live copies so far: a boot catch-up verified 21:07:35Z and the first on-the-hour copy at 22:00:11Z. API-only change, no picture.
**Your call:** None.

## Decided
- [dc_j4b3u1r7z6](2026-10-31-gr-ba0juhlm7n-funded-three-steps-queued-hourly-ver-b3u1r7z6.md) (Cleo, grant funded: three steps queued) → approve.
- [dc_b2rozj8fzj](2026-10-31-gr-ba0juhlm7n-step-1-town-db-now-copied-off-site-e-rozj8fzj.md) (Cleo 1, step 1: PR #195 merged as 87fd69b) → approve.
- [dc_ahr3tqmp6n](2026-10-31-gr-ba0juhlm7n-step-2-parked-until-hourly-backups-8-r3tqmp6n.md) (Cleo 1, step 2 parked until 87fd69b live) → approve.
No new reports since rollup #26.

## Key results
gr_ba0juhlm7n (checkpoint, ~157,000 / 150,000):

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_bd08a0607a unit tests: hourly schedule, boot catch-up > 1 h, retention 48 + 30, verify fails loudly on a corrupted object | claimed | npm test in packages/server (test/backup.test.ts) green in the PR's CI | All four cases are on main under exactly those names; PR #195 CI green; 87fd69b is an ancestor of the live commit ae18eb3 |
| kr_cee8c26801 live cadence: copies land every hour for a day | on-track | health backup.lastAt and verifiedAt at the next morning check, both < 70 min old, error null | Two verified copies (21:07:35Z catch-up, 22:00:11Z on the hour) in the first ~75 min live; a full day runs out at the 11-01 05:05Z morning check |
| kr_1a69c0a3be live cost: the hourly run doesn't stall the server | not-started | health load.lagMs under 200 ms during a run; no lag FYI on the Prod board that day | Not measurable yet: the only on-the-hour run (22:00Z) fell inside the 21:19–22:10Z RED lag window from the restart storm ([dc_72813k29cz](../../fyi/2026-10/2026-10-31-cleared-red-lag-event-loop-lag-p99-39-ms-813k29cz.md)), which is not the backup's doing. Clean sample now: 74 ms |
| kr_y7u2m9hk9y at most 1 h of town state lost if the Fly volume dies | on-track | health backup.lastAt never > 70 min old over a day; bucket lists hourly objects; README "Drill" records a restore of an hourly copy with MATCH | Hourly half live and verified; the day of cadence and the drill from an hourly copy (the recorded drill of 10-28 used a nightly object) are still owed |

Where the tokens went: funding session 26,957 ([dc_j4b3u1r7z6](2026-10-31-gr-ba0juhlm7n-funded-three-steps-queued-hourly-ver-b3u1r7z6.md)); step 1 engineering 77,332 ([dc_b2rozj8fzj](2026-10-31-gr-ba0juhlm7n-step-1-town-db-now-copied-off-site-e-rozj8fzj.md)); step 2 parked 13,212 ([dc_ahr3tqmp6n](2026-10-31-gr-ba0juhlm7n-step-2-parked-until-hourly-backups-8-r3tqmp6n.md)); step 2's resumed run about 39,000, cut by the 21:30:06Z restart storm before it could file a report (the work it did is lost); this checkpoint about 15,000. The engineering came in on plan; the overrun is the cut session.

Other funded grants:

| Grant | Key results | Spent / granted |
|---|---|---|
| gr_z2v838adk9 dead-volume recovery (checkpoint, rollup #26 [dc_hexmsgulr1](2026-10-31-prod-rollup-26-checkpoint-gr-z2v838adk9-dead-volum-xmsgulr1.md)) | kr_17cd844e42, kr_cc9dc81c96 on-track (PR #210, CI rerunning); kr_7svvwv6lr5 at-risk; kr_36d053ac89, kr_ccca476c37 not-started | 182,768 / 160,000 |
| gr_w9ue1k1p0c redeploys keep team-lead sessions | kr_ohom5phapo, kr_245c17e700, kr_11595f1ae5, kr_9b2712691e: all not-started (steps 1-2 live, PR #212 queued to merge, daily check from 11-02) | 347,089 / 500,000 |

Today's spend by lane: exploration 211,986 tokens (free under the goal: 201,862), directed 0 tokens.

## Needs from Mitchell
1. Continue the hourly-backup grant with about 65,000 more tokens: step 2 (~40k: sample lag across a top of the hour, restore from the latest hourly copy on a throwaway, record it in README "Drill", one small PR) and step 3 (five daily clean-day checks at ~5k each, then the close). Why: the feature is live and working; what's left is the proof the key result asks for. If you'd rather stop here, adjust to ~10k and I'll close it with the cadence and cost key results checked at the next morning check only and the hourly-copy drill missed.

_Already waiting in your in-tray: 0 proposals, 1 request ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), 1 rollup ([dc_hexmsgulr1](2026-10-31-prod-rollup-26-checkpoint-gr-z2v838adk9-dead-volum-xmsgulr1.md))._
