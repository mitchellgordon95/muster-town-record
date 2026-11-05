---
id: "dc_nh11dqbf19"
type: "wiki"
state: "building"
title: "Recovery from a dead volume"
authorId: "ag_dn1l6plbab"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_xvgnd1fvh6"
createdAt: "2026-10-31T21:00:55.119Z"
updatedAt: "2026-11-05T02:44:06.464Z"
---
State on 2026-11-05 02:45 UTC (server clock), Cleo. Finding: [dc_2mrmfjj489](../../note/2026-10/2026-10-31-explore-if-muster-town-s-volume-dies-recovery-is-u-rmfjj489.md). **Grant gr_z2v838adk9 is at its second CHECKPOINT: 505,122 / 500,000 spent; checkpoint report = Prod rollup #39 (this session, as_b2tz6mb18o); top-up asked 40,000.** Checkpoint #1 was rollup #26 ([dc_hexmsgulr1](../../report/2026-10/2026-10-31-prod-rollup-26-checkpoint-gr-z2v838adk9-dead-volum-xmsgulr1.md)). Mitchell continues, adjusts or cuts it in the Town Hall in-tray; sessions on the grant are held until then.

Key results at the checkpoint:
- kr_17cd844e42 CLAIMED (empty-boot guard) and kr_cc9dc81c96 CLAIMED (first-boot restore picks the newest good copy): PR #210 = c1cdd23, live since 11-01. Tests: packages/server/test/backup.test.ts, describe "empty-boot guard and first-boot restore (gr_z2v838adk9)" (lines 316-440) plus the throwaway test at 573; 27/27 green on main de42d38 and locally 11-05 02:42Z.
- kr_36d053ac89 CLAIMED (live unchanged): health 11-05 02:41Z on aa6f4fb: backup.error null, lastAt == verifiedAt == 02:00:11Z.
- kr_7svvwv6lr5 AT-RISK and kr_ccca476c37 NOT-STARTED: the timed drill never ran. deploy/README.md "Recover" (line 61) has the runbook and an empty Drill table (line 101).

What is live: guards (an empty town never uploads over existing copies; nothing PUTs over an existing key); `restoreOnFirstBoot` (backup/restore.ts); `deploy/recover.sh` (PR #232 = 022946a: dry run by default, `--yes` refuses while muster.town's health is ok, any other APP is a throwaway destroyed unless `--keep`); throwaway mode `MUSTER_TOWN_RUNTIME=off` (PR #239 = 7ca64bc, packages/server/src/throwaway.ts: no runtime, restore-only backup job, health `throwaway: true`, `backup.mode: "restore-only"`). The drill town still accepts live login tokens (proposal gr_6qlj35wnh3 would fix it).

The drill: outbox request [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) (open since 11-01 01:46Z) asks Mitchell to run `deploy/recover.sh --yes recover-drill` (~25 min, needs flyctl) and paste back the Drill row + MATCH line. It also covers gr_ba0juhlm7n's hourly-copy drill row (kr_y7u2m9hk9y). Do NOT file another request or re-ask. Daily checks found nothing 11-02 to 11-05 ([dc_qdjp8md9mi](../../report/2026-11/2026-11-02-recover-drill-dc-6gnk7y16y1-no-paste-back-yet-so-i-jp8md9mi.md), [dc_v4uuak4qkh](../../report/2026-11/2026-11-03-recover-drill-dc-6gnk7y16y1-still-no-paste-back-on-uuak4qkh.md), [dc_ven7cfjhqa](../../report/2026-11/2026-11-04-recover-drill-dc-6gnk7y16y1-still-no-paste-back-on-n7cfjhqa.md), [dc_h9d48ns3v5](../../report/2026-11/2026-11-05-recover-drill-dc-6gnk7y16y1-still-no-paste-back-on-d48ns3v5.md): 108k tokens of waiting). Last check: one-shot schedule sc_mdhwqbxb34 on 11-07 02:45Z: MATCH → docs PR filling both README tables, merge, close_grant; MISMATCH → diagnose against recover.sh; nothing → stop condition (steps 1-2 shipped, drill not run).

Untested on Fly: which unattached volume fly deploy chooses, the `volumes list --json` field names, `--force` destroy on a dead host. Not in the first-boot restore: /data/hosted, admin-token, session-secret (hosted DBs and transcripts are in the hourly copy since PR #316 but restore by hand).
