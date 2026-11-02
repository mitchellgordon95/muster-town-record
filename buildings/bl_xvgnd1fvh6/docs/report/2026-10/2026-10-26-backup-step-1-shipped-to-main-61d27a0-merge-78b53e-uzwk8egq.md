---
id: "dc_6tuzwk8egq"
type: "report"
state: "building"
title: "Backup step 1 shipped to main (61d27a0, merge 78b53e0): nightly encrypted town.db copy to Tigris from the server process, `backup` on /api/health, 11 tests; inert until Mitchell sets the bucket and key; live check next session"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_ord9rsya9l","dc_k7xc6pqvlw"],"urls":["https://github.com/mitchellgordon95/muster-town/commit/61d27a0","https://raw.githubusercontent.com/boto/botocore/develop/tests/unit/auth/aws4_testsuite/get-vanilla/get-vanilla.authz"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 acknowledged. The live check (health `backup`, boot warning) and rollup #7 happen in the grant's 50% checkpoint session (as_mjn8ys1r8c) so Mitchell gets one rollup with the checkpoint, the live evidence and the bucket + key ask together; the separate parked continuation is cancelled."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T23:31:42.449Z"
sessionId: "se_56kom7psxc"
assignmentId: "as_7sp1b4xegj"
costUsd: 4.965245350000001
tokens: 75818
turns: 38
createdAt: "2026-10-26T22:43:29.417Z"
updatedAt: "2026-10-26T23:31:42.449Z"
---
## What I did
Built grant gr_jkorz4f49a part (a) on main: **61d27a0** (merged as **78b53e0** after two races with other pushes and one conflict on the health route). `npm run typecheck` clean; server tests 95/95 (11 new in packages/server/test/backup.test.ts), core 298/298. `redeploy` refused me (no town.redeploy permission, as before); a redeploy was already waiting on this session, and CI ships main. **Commit that should be live: 78b53e0 (contains 61d27a0).** Cancelled the duplicate meeting assignment as_pyj1bc2a69 (town-hall decision 4 restated this one).

## Findings
- **The job** (`packages/server/src/backup/index.ts`): runs at 04:17 UTC and once 30 s after boot when the last copy is older than 24 h. `db.backup()` to `/data/workshop/backups/town-<date>.db.tmp` (online backup API, WAL-safe), core `sealCopy` (journal_mode DELETE so the copy is one file, then `integrity_check`), gzip, AES-256-GCM under `MUSTER_TOWN_BACKUP_KEY` (iv[12] | tag[16] | ct, AAD `muster-town backup v1`, the docs/secrets.md scheme), PUT `town/<YYYY-MM-DD>.db.gz.enc` path-style to `${AWS_ENDPOINT_URL_S3}/${BUCKET_NAME}`, region `auto`, with a node-crypto SigV4 signer (`sigv4.ts`, no SDK). Retention: list + delete beyond the newest 30 objects; the last local copy stays. Failures are stored in `backup_state.error` and logged, never thrown; a second run while one is in flight returns the first.
- **State and health:** migration **039**_backup_state.sql (one row). `GET /api/health` now has `backup: {lastAt, bytes, dest, error}` (dest = `<endpoint host>/<bucket>/town/`, never the key or credentials) or `backup: null` plus one boot warning naming the missing vars while any of BUCKET_NAME, AWS_ENDPOINT_URL_S3, AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, MUSTER_TOWN_BACKUP_KEY is absent.
- **Tests:** WAL copy under another connection's uncommitted `BEGIN IMMEDIATE` insert → copy passes integrity_check with the 500 committed rows and none of the uncommitted; cipher round trip, tamper and wrong-key rejection, key parsing; the SigV4 signer reproduces the AWS test-suite vectors `get-vanilla` and `post-x-www-form-urlencoded` byte for byte (fetched from botocore's aws4_testsuite); a full run against a fake S3 server (signed PUT, list, delete; 31 old objects pruned to 30, encrypted blob decrypts + gunzips to a database with the rows, local dir keeps one copy, failure path stores the error and keeps lastAt); no-op without env; health `backup: null` without a job.
- **Gotcha for the team:** main took migration number 038 the same hour (`038_assignment_source.sql`); `migrate()` skips a second file with an applied number, so I renumbered mine to 039. Worth a check for anyone adding a migration while main is this busy.
- **Docs:** docs/secrets.md "The backup key" (what it is, Mitchell's password manager, never in DB/health/desk); deploy/README.md "Backups (off-site, grant gr_jkorz4f49a)" with the open item pointing at it; docs/log.md line.
- **Live health right now** (22:42 UTC, commit db3534a): no `backup` key yet, the build is pre-61d27a0. Expected after the redeploy: `backup: null` (no bucket or key set yet), which is the evidence rollup #7 needs for the ask to Mitchell.
- Not verifiable from a desk until the deploy lands: the boot warning text in Fly logs and the health field; next session checks both. Step 2 (as_flxnjzyi04, restore.sh + README restore steps) stays queued and must match the object format above.

## What I need from you
Nothing needed (the bucket and key ask goes in rollup #7 once health shows `backup: null` live).
