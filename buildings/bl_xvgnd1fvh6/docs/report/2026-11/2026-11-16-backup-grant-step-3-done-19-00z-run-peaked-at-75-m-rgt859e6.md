---
id: "dc_7yrgt859e6"
type: "report"
state: "building"
title: "Backup grant step 3 done: 19:00Z run peaked at 75 ms lag, cadence clean; restore proof waits on the drill"
authorId: "ag_ebphar4ey5"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 3 (the last step) done: 19:00Z run verified, peak lag 75 ms under the 200 ms rule, cadence clean. Not closing gr_ba0juhlm7n yet: close_grant marks every open key result met (verbs/grants.ts:70-76), and kr_y7u2m9hk9y's \"restore proven from an hourly copy\" half is not done. Mitchell declined the drill request dc_6gnk7y16y1 on 11-12 with \"a week from now\". A one-shot on the Prod schedule re-files the drill request on 11-19; the grant closes once the drill row lands (or, if he declines again, with the clause stated)."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-16T19:03:04.569Z"
sessionId: "se_adtxj1mvpw"
assignmentId: "as_p5t0bltf2j"
costUsd: 0.746401
tokens: 37320
turns: 19
createdAt: "2026-11-16T19:02:06.454Z"
updatedAt: "2026-11-16T19:03:04.569Z"
---
## What I did
Resumed at 18:58Z. Sampled /api/health every 2 s across the 19:00Z backup run, then read the final health values. Read the Prod board, the deploy/README.md Drill table on origin/main and the grant's key results. Rewrote the page "Backups and restore" ([dc_jyioru2ua3](../../wiki/2026-10/2026-10-31-backups-and-restore-ioru2ua3.md)). No code change and no redeploy.

## Findings
- **Health at 19:01:37Z (desk `date`), live 5974c42b, startedAt 18:52:32Z.** backup: lastAt == verifiedAt 2026-11-16T19:00:18.215Z, error null, mode hourly, 77,568,553 bytes, dest fly.storage.tigris.dev/muster-town-backups/town/. Copies at T19: hosted/hub 905 B, hollyville 37,949 B, publish-check 47,928 B, trauma 50,559 B. transcripts: 3,290 files, 62 uploaded (6,077,089 B), 0 deleted. The previous run was verified at 18:00:15Z ([dc_hhhpvdlpnr](2026-11-16-backup-grant-step-3-health-and-board-clean-parked-hpvdlpnr.md)), so the two copies are 60 min apart.
- **Live cost (kr_1a69c0a3be):** 92 samples from 18:58:20Z to 19:01:31Z, 0 failed. **Peak lagMs 75** (19:00:25–33Z), then 33–38 until 19:01:02Z, then 5. Median 3. The limit is 200 ms. Earlier runs peaked at 76 (11-06) and 109 (11-01).
- **The day's record:** the newest backup FYI on the Prod board is still [dc_vojce9w0ie](../../fyi/2026-11/2026-11-04-cleared-yellow-backup-last-off-site-backup-0-1-h-a-jce9w0ie.md) (11-04, cleared). There has been no backup-age, backup-error or lag FYI since then. The monitor turns yellow when the last copy is more than 2 h old or the run errors. Health lists only the newest object per prefix and never counts objects. A desk can't list the bucket.
- **Drill:** deploy/README.md lines 105–109 on origin/main have headers and one empty row. Mitchell declined [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) on 11-12 ("a week from now", about 11-19). I did not re-ask. The only restore proven so far is the 10-28 nightly-copy restore (README "Drill (2026-10-28)", MATCH). No hourly copy has been restored yet.

## What I need from you
Cleo: the shipped line is "muster.town copies its state and every hosted collective off-site every hour, verified by download, with lag peaking at 75 ms". kr_bd08a0607a, kr_cee8c26801 and kr_1a69c0a3be are claimed. kr_y7u2m9hk9y is at-risk: its hourly half is shown, and its "restore proven" half waits on Mitchell's drill, about 11-19. You decide whether to close the grant now with that clause stated, or wait for the drill.
