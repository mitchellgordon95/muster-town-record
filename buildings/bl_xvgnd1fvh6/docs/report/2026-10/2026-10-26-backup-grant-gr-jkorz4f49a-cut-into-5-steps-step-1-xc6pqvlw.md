---
id: "dc_k7xc6pqvlw"
type: "report"
state: "building"
title: "Backup grant gr_jkorz4f49a cut into 5 steps; step 1 (server job, health `backup` field, tests, inert without secrets) assigned to me as as_7sp1b4xegj, step 2 (restore.sh + README) queued behind it as as_flxnjzyi04; steps 3–5 wait on Mitchell's bucket and key"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_ord9rsya9l"],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged: the plan's steps 1 (as_7sp1b4xegj) and 2 (as_flxnjzyi04) are already assigned, so no new assignment from this report. Steps 3–5 get assigned once step 1 is live and health shows whether Mitchell's bucket and key exist."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T22:04:51.561Z"
sessionId: "se_cp0fqggdk7"
assignmentId: "as_p290jxl92v"
costUsd: 1.4300240999999998
tokens: 13239
turns: 13
createdAt: "2026-10-26T22:04:31.410Z"
updatedAt: "2026-10-26T22:04:51.561Z"
---
## What I did
Read the funded plan and its findings doc [dc_ord9rsya9l](../../note/2026-10/2026-10-26-off-site-backup-for-town-db-destination-comparison-d9rsya9l.md), checked the live state (health commit 61932f2 = main head, no `backup` field yet; the health route in packages/server/src/routes/town.ts, WAL mode in core/src/db.ts, the Backups open item in deploy/README.md), cut the plan into five steps and assigned the two that need no secrets. No code change this session.

## Findings
Steps, one owner each (me: Dara is stopped and has no page on this):
1. **as_7sp1b4xegj (assigned, lane grant):** the nightly job in the server process (04:17 UTC + boot catch-up when the last copy is > 24 h): `db.backup()`, integrity_check, gzip, AES-256-GCM with MUSTER_TOWN_BACKUP_KEY, SigV4 PUT to the Tigris bucket as town/<date>.db.gz.enc, 30 objects kept, state table, read-only `backup: {lastAt, bytes, dest, error}` on /api/health (null + boot warning without the five secrets, so inert until set), tests (WAL copy with an uncommitted writer, encrypt round trip, signer vector, no-op without env). Push to main, redeploy. Check: health has a `backup` key; the server tests include the WAL-writer test.
2. **as_flxnjzyi04 (queued, waits on step 1):** scripts/backup/restore.sh (download, decrypt, integrity_check, RESTORE.tgz via the entrypoint's path onto a scratch app, compare counts, destroy; a --local mode) and the README "Backups" section; open item dropped. Check: README section present, open item gone.
3. **Verify the first object** (assign once health shows `backup.lastAt`): lastAt < 24 h, bytes > 0; rollup.
4. **Restore drill** on scratch app muster-town-restore, agent count + newest doc createdAt vs live, destroy, report. Needs a Fly token that can create apps (FLY_STRESS_TOKEN was to be revoked after the stress grant) and the five secrets on the desk, or Mitchell runs restore.sh from his Mac.
5. **Three-night confirmation**: three consecutive objects and three days of health < 24 h, then the final report; stop condition met.

Mitchell's part (from the grant note, not checkable from a desk): `fly storage create -a muster-town` and `fly secrets set MUSTER_TOWN_BACKUP_KEY=...` kept in his password manager. Step 1's report will say whether health shows `backup: null` after the deploy; if so, rollup #7 asks for the two commands. The grant's 7-day inert clock ends 2026-11-02.

## What I need from you
Nothing needed (the bucket and key request goes in the next rollup once step 1 is live and health shows whether they exist).
