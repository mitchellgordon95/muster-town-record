---
id: "dc_os03yc6vtm"
type: "report"
state: "building"
title: "Wiki harvested: 5 Prod topic-page drafts (monitor internals, VPS pinger, backup internals, desk slots, secrets/tokens), ready for Cleo to publish"
authorId: "ag_8uq6fnjis4"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_k93qotuwrg","dc_88n5qc4t1x","dc_t1vee69sou","dc_stx4kn4dto","dc_qfrf3imq52","dc_9w92tzhem6","dc_z22wolxdnu"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Harvest done: 5 drafts (dc_k93qotuwrg, dc_88n5qc4t1x, dc_t1vee69sou, dc_stx4kn4dto, dc_qfrf3imq52), each under 2,500 chars and rechecked against 2d8694d. Cleo publishes them as Prod topic pages in as_pxvtpf7756 and tells Mitchell step 1 is done."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T03:50:54.640Z"
sessionId: "se_9ijd5vvaop"
assignmentId: "as_w73g2mspqw"
costUsd: 0.9356595000000002
tokens: 46783
turns: 28
createdAt: "2026-10-29T03:50:31.734Z"
updatedAt: "2026-10-29T03:50:54.640Z"
---
## What I did
- Read my four wiki pages and Cleo's published topic page "Monitoring and alerting" ([dc_9w92tzhem6](../../wiki/2026-10/2026-10-29-monitoring-and-alerting-92tzhem6.md)). The other four topic pages named in the assignment (Off-site backup, Fly deployment, Stress test, Prod working rules) weren't published yet when I searched.
- Rechecked each fact against main 2d8694d and live health. Health at 03:50Z showed commit 2d8694d, outbound false, alerts [], and backup.lastAt 2026-10-28T17:10:02.951Z.
- Wrote 5 notes, all filed in the building and each under 2,500 characters. Where Cleo's page or deploy/README.md already covers a topic, the draft points to it and adds only what they don't have.
- No code and no commits.

## Findings
**The five drafts:**

| Draft | Topic |
|---|---|
| [dc_k93qotuwrg](../../note/2026-10/2026-10-29-topic-page-draft-monitor-internals-monitor-ts-coun-3qotuwrg.md) | **Monitor internals.** Functions and files in monitor.ts, main.ts, app.ts, ws.ts and routes/town.ts. Outbound is decided once at boot. State lives in the meta row 'monitor' and survives restarts. The gap event. The 10/h cap counts the test endpoint too. Test file, commands, commits. Written as additions to [dc_9w92tzhem6](../../wiki/2026-10/2026-10-29-monitoring-and-alerting-92tzhem6.md). |
| [dc_88n5qc4t1x](../../note/2026-10/2026-10-29-topic-page-draft-vps-pinger-on-wright-s-box-n5qc4t1x.md) | **VPS pinger on Wright's box.** Host and user, script path, unit and timer names, env and state files, install commit (49e2622, not yet 36e8227), what Wright can and can't do, the healthy journal line, the dead-URL test, the dry-run trick. |
| [dc_t1vee69sou](../../note/2026-10/2026-10-29-topic-page-draft-backup-internals-and-restore-sh-vee69sou.md) | **Backup internals and restore.sh.** The files in packages/server/src/backup/, the 5 env vars, the tests, the 22dabd1 fixes, the drill, and the link to the monitor's backup metric. Written as additions to Cleo's "Off-site backup" page. |
| [dc_stx4kn4dto](../../note/2026-10/2026-10-29-topic-page-draft-desk-slots-and-desks-maxrunning-x4kn4dto.md) | **Desk slots / desks.maxRunning.** Schema and default, the stored value 6, how to change it live, where to read it, and the decision trail. |
| [dc_qfrf3imq52](../../note/2026-10/2026-10-29-topic-page-draft-secrets-and-tokens-open-work-for-rf3imq52.md) | **Secrets and tokens.** Current state plus the open work behind kr_wm6mphmrjf. |

**Things that changed since my notes, and are corrected in the drafts:**
- The DESK_ENV_ fallback is gone (f192db1).
- Token hashing ("PR 2") never landed: tokens are still plaintext in the `tokens` table.
- The "6 desks" limit came from the old OVH stress test ([dc_vxgg8r55ha](../../note/2026-10/2026-10-21-stress-test-how-many-desks-muster-prod-1-ovh-d2-8-gg8r55ha.md)), not the Fly Machine.

**Check on Cleo's page:** the first scheduled nightly backup is due at 2026-10-29 04:17Z. Until it runs, health still shows the 10-28 17:10Z boot copy.

**Left out on purpose:**
- Run-by-run history: CI run ids, the cancelled d33e446 run, session crash and retry details.
- The 2026-10-27 live-bundle check.
- My personal desk workflow, apart from the tsc and vitest commands.
- Any contact details or secret values.
- The stored maxRunning value hasn't been rechecked since 2026-10-27, and the draft says so.

## What I need from you
Nothing needed.
