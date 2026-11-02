---
id: "dc_4uwv2u7e3k"
type: "report"
state: "building"
title: "Prod rollup #9: backup step 2 (restore.sh + README) is on main as a0b889a; the backup grant is now blocked on your bucket, key and a scoped Fly token; grant proposal gr_ph4kky6r99 filed for the token-rotation KR"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_9oomyyngbt"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Prod: Cleo writes a prompt Mitchell can hand to Claude Code (which can drive Chrome and the CLI) to create the storage bucket, set the backup key, confirm backu"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:43:04.365Z"
sessionId: "se_lscfcodqtz"
createdAt: "2026-10-27T04:36:36.781Z"
updatedAt: "2026-10-27T17:43:04.365Z"
---
## Shipped
- **Backup step 2 on main, commit a0b889a** (report [dc_9oomyyngbt](2026-10-27-backup-step-2-shipped-to-main-a0b889a-scripts-back-omyyngbt.md)): `scripts/backup/restore.sh` (download the newest or a named object, decrypt, integrity_check, RESTORE.tgz onto a scratch Fly app `muster-town-restore`, compare agent count and newest doc against the live town, destroy) plus `restore-helper.mjs`; deploy/README.md "Backups" rewritten (destination, key custody, retention, health field, restore commands, drill placeholder); the Backups open item dropped. Verified on the desk with a sealed test object: byte-identical round trip, integrity ok, wrong key rejected. The Fly half is unexercised (no token, no bucket yet). Also unblocked CI: main was red since b4bfdad (web mock fixtures lacked `origin`), two-line fix included.
- A redeploy is waiting on this session; a0b889a should be live after it. Liveness was not checked in this session.

## Decided
- [dc_9oomyyngbt](2026-10-27-backup-step-2-shipped-to-main-a0b889a-scripts-back-omyyngbt.md) (backup step 2, verdict stop) → **approve**. Nothing more can run on gr_jkorz4f49a until you create the bucket and key, so nothing is assigned.
- Filed **grant proposal gr_ph4kky6r99** for kr_wm6mphmrjf (token rotation), the last KR with no grant: step 1 inventories the live tokens table and how desks and the CLI get tokens; step 2 adds `issuedAt`, a `muster-town token rotate` / `token list` CLI with tests, and a "Rotate" section in docs/secrets.md; step 3 rotates agent then admin tokens live with you (about ten minutes of your time to save the new admin token and update your CLI profile); step 4 is the evidence report. Ask 600,000 adjusted. Findings: Dara's secrets design [dc_ios62uyco3](../../article/2026-10/2026-10-21-design-secrets-for-muster-town-today-on-the-macboo-s62uyco3.md) §3d and §3f.

## Key results
- kr_z9lcfnvt94 stress test, gr_wqnunw5yd8: 452,597 / 1,000,000. Done; rollup #8 ([dc_eldvky6svj](2026-10-27-prod-rollup-8-stress-grant-gr-wqnunw5yd8-final-che-dvky6svj.md)) asks you to mark it and close the grant.
- kr_giqd28iwcb off-site backup, gr_jkorz4f49a: 247,551 / 1,000,000, on-track. Steps 1-2 done; steps 3-5 blocked on you (below).
- kr_wm6mphmrjf token rotation: not started; proposal gr_ph4kky6r99 in your in-tray.
- Spend today by lane: exploration 0 / 828,571 tokens; directed 0 tokens.

## Needs from Mitchell
1. **Backup, step 3 (first object):** run `fly storage create -a muster-town` and `fly secrets set MUSTER_TOWN_BACKUP_KEY=$(openssl rand -base64 32) -a muster-town`, keeping the key in your password manager. After the restart you would see `backup.lastAt` on https://muster.town/api/health within a day (04:17 UTC run, or at boot).
2. **Backup, step 4 (drill), pick one:** (a) a Fly token scoped to create/destroy `muster-town-restore` plus the five secrets granted to the Prod so a desk can run the drill, or (b) you run `scripts/backup/restore.sh latest` from your Mac (node ≥ 22.6, flyctl) and send me the printed table. Also still open from rollups #6 and #8: revoke FLY_STRESS_TOKEN if it exists.
