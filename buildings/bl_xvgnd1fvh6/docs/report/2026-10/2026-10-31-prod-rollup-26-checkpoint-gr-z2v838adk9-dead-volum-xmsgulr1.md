---
id: "dc_hexmsgulr1"
type: "report"
state: "building"
title: "Prod rollup #26 (checkpoint gr_z2v838adk9): dead-volume recovery is one third built, over budget by 23k because a repeated manager session was charged to it; asking ~110k to finish"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_0z80k3w8hw","dc_zi69pv4wa8"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-01T00:46:33.298Z"
sessionId: "se_we1lsu20pb"
assignmentId: "as_kfigfg2md9"
costUsd: 2.417279249999999
tokens: 48346
turns: 30
createdAt: "2026-10-31T22:19:40.852Z"
updatedAt: "2026-11-01T00:46:33.298Z"
---
Live cbe1bf1 since 22:07Z (health at 22:13:57Z: backup lastAt == verifiedAt == 22:00:11Z, error null, no monitor alerts, lag 11 ms). This is the 100% checkpoint for gr_z2v838adk9 (dead-volume recovery), 182,768 / 160,000 tokens.

## Shipped
Nothing from this grant is live yet. Step 1 is written and tested in PR #210 (https://github.com/mitchellgordon95/muster-town/pull/210, draft, head b9cdff4): the empty-boot guard (a fresh town with copies in the bucket refuses to upload and goes red in the monitor; a run never overwrites an existing object) and first-boot restore (a server with no town.db and the backup secrets starts from the newest copy that decrypts and passes an integrity check, skipping corrupt ones). Its first CI run failed only on a Machine-size test that main had already fixed, so I merged main into the branch at 22:17Z; typecheck and all 239 server tests pass locally and CI is rerunning. Merge, redeploy and the live check are queued (as_wp3cuxl7tx) and held by this checkpoint.

## Decided
- [dc_zi69pv4wa8](2026-10-31-gr-z2v838adk9-step-1-backup-guards-first-boot-rest-69pv4wa8.md) (Cleo 1, step 1: PR #210, parked on CI) → approve.
- [dc_0z80k3w8hw](2026-10-31-gr-z2v838adk9-funded-repeat-its-three-steps-were-a-80k3w8hw.md) (Cleo, repeated "grant funded" session; found the 21:09–21:47Z restart storm) → approve.

## Key results
gr_z2v838adk9 (checkpoint, 182,768 / 160,000):

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_17cd844e42 empty-boot guard | on-track | packages/server test: bucket with town/…T20 object + fresh db → run() refuses, backup.error set, monitor red, object unchanged | Exactly that test is in PR #210 (backup.test.ts "empty-boot guard and first-boot restore", monitor.test.ts); green locally on b9cdff4, CI rerunning; not on main |
| kr_cc9dc81c96 first-boot restore picks the newest good copy | on-track | test with a corrupt newest object and a good older one: server starts with the good copy's agent count | In PR #210: corrupt newest + non-database middle + good older copy → restored with the good copy's agent count, no seeding; green locally; not on main |
| kr_36d053ac89 live unchanged after merge | not-started | health after the redeploy: backup.error null, lastAt == verifiedAt, < 70 min old | Not merged yet. Baseline now: lastAt == verifiedAt == 22:00:11Z, error null |
| kr_ccca476c37 timed recovery drill | not-started | README "Recover": volume-created → health-ok ≤ 30 min, agent count and newest doc match | No recover.sh or drill yet (steps 2 and 3 queued, held) |
| kr_7svvwv6lr5 30-min one-command recovery, fresh volume can't bury good copies | at-risk | README "Recover" drill ≤ 30 min; guard tests green on main | Guard half proven on the PR branch; recovery half not started. At risk on budget, not on the work |

Where the tokens went: step 1 engineering ~75.7k ([dc_zi69pv4wa8](2026-10-31-gr-z2v838adk9-step-1-backup-guards-first-boot-rest-69pv4wa8.md)); a repeated "grant funded" team-lead session ~87.9k ([dc_0z80k3w8hw](2026-10-31-gr-z2v838adk9-funded-repeat-its-three-steps-were-a-80k3w8hw.md)) that mostly investigated the 21:09–21:47Z restart storm, charged to this grant because the funding assignment fired twice; this checkpoint ~19k.

Other funded grants:

| Grant | Key results | Spent / granted |
|---|---|---|
| gr_w9ue1k1p0c redeploys keep team-lead sessions | kr_ohom5phapo, kr_245c17e700, kr_11595f1ae5, kr_9b2712691e: all not-started (steps 1-2 live, PR #212 for the 21:30Z cut queued to merge, daily check from 11-02) | 347,089 / 500,000 |
| gr_ba0juhlm7n hourly encrypted backups | kr_y7u2m9hk9y, kr_bd08a0607a, kr_cee8c26801, kr_1a69c0a3be: checkpoint already filed, waiting on your decision | 156,707 / 150,000 (checkpoint) |

Today's spend by lane: exploration 211,986 tokens (free under the goal: 0), directed 0 tokens.

## Needs from Mitchell
1. Continue gr_z2v838adk9 with about 110,000 more tokens (merge PR #210 and the live check ~15k, deploy/recover.sh plus README "Recover" ~55k, one timed drill on a throwaway app ~40k). Why: the work itself is on plan at ~76k for step 1; the overrun is a duplicated manager session, not the recovery work. If you'd rather stop at the guard and first-boot restore, adjust to ~20k and I'll merge step 1 and close the grant with the drill key results missed.

_Already waiting in your in-tray: 0 proposals, 1 request ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), 0 rollups._
