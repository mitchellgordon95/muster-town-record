---
id: "dc_45u8oy7e61"
type: "report"
state: "building"
title: "Prod rollup #7 (checkpoint gr_jkorz4f49a, 50%): backup step 1 is merged with tests but not live (CI on main was red since 6105e18; fixed in 9f72eaa); KR on-track, 2,671,703 / 4,000,000; continue the grant and create the Tigris bucket + backup key"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_k7xc6pqvlw","dc_6tuzwk8egq"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Prod backup: Mitchell continues gr_jkorz4f49a and creates the storage bucket and backup key. Cleo: check the deployed fix and that /api/health shows the backup"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T03:57:14.483Z"
sessionId: "se_de0b6d9zmp"
assignmentId: "as_mjn8ys1r8c"
costUsd: 2.1402002500000004
tokens: 34021
turns: 24
createdAt: "2026-10-26T23:36:01.684Z"
updatedAt: "2026-10-27T03:57:14.483Z"
---
## Shipped
- **Backup step 1 in main, not yet live:** 61d27a0 (merge 78b53e0). Nightly encrypted town.db copy from the server process to a Tigris bucket (04:17 UTC + boot catch-up), AES-256-GCM per object, SigV4 S3 client, 30-object retention, read-only `backup` on /api/health, migration 039. 11 tests in packages/server/test/backup.test.ts. docs/secrets.md "The backup key"; deploy/README.md "Backups". Inert until the five env vars exist (AWS_* + BUCKET_NAME from `fly storage create`, MUSTER_TOWN_BACKUP_KEY).
- **CI on main unbroken:** 9f72eaa (merge 3d329e2). Main had been red since Lena's 6105e18 (Bank step 3) at 22:31: the runtime proxy-chat test still expected 40 raw tokens where the Bank now books 960 adjusted (20 in + 20 out on Opus priced at list, expressed in Haiku output tokens, as docs/bank.md says). Nothing was deploying for an hour (health commit db3534a). The runtime test file passes locally (12/12). **Should be live after the next green run: 3d329e2** (contains 61d27a0 and a848d7b). I'll verify next session.

## Decided
- [dc_k7xc6pqvlw](2026-10-26-backup-grant-gr-jkorz4f49a-cut-into-5-steps-step-1-xc6pqvlw.md) (grant cut into 5 steps): approved; steps 1 and 2 queued to me.
- [dc_6tuzwk8egq](2026-10-26-backup-step-1-shipped-to-main-61d27a0-merge-78b53e-uzwk8egq.md) (step 1 shipped): approved; live check folded into this checkpoint.
- The live check found the deploy blocked by red CI; I fixed the test on main rather than wait (standing rule: push to main). Steps 3–5 stay unassigned until the bucket and key exist.

## Key results
- **kr_giqd28iwcb** (off-site backup): **on-track**, 2,671,703 / 4,000,000 tokens. How to check now: once /api/health's commit contains 3d329e2, it shows `backup: null` (no secrets yet) and the boot log has one warning naming the missing vars. Testing plan: WAL-safe copy = test passes (uncommitted writer, integrity_check ok, committed counts); encrypted objects, health lastAt, restore drill, three nights = not yet possible (no bucket); procedure = README Backups section written, restore commands come with step 2 (held).
- kr_z9lcfnvt94 (stress, gr_wqnunw5yd8): work complete at 9,847,502 / 10,000,000; still waiting for you to mark it met or cut the grant (rollup #6).

## Needs from Mitchell
1. **Continue gr_jkorz4f49a**, and create the bucket and key: `fly storage create -a muster-town` (sets AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_ENDPOINT_URL_S3, BUCKET_NAME) and `fly secrets set MUSTER_TOWN_BACKUP_KEY=$(openssl rand -base64 32) -a muster-town`, keeping the key in your password manager. Without them the grant is inert and its stop condition fires 7 days after funding.
2. For the restore drill (step 4): a Fly token scoped to a scratch app `muster-town-restore`, or tell me you'll run scripts/backup/restore.sh from your Mac and I'll write it for that.
