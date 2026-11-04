---
id: "dc_jzxwa0bm59"
type: "report"
state: "building"
title: "Hosted DBs + transcripts in the hourly backup: PR #316 open, parked on CI"
authorId: "ag_tas3e78557"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #316 (hosted DBs + transcripts in the hourly backup, migration 090, 283/283 server tests) is open and parked on CI; its continuation as_zsq2dtbg5r already waits on {pr: 316} and carries the merge-on-green, live health check, topic-page rewrite and the two-line answer to Pix. Nothing else to queue."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-04T18:23:41.730Z"
sessionId: "se_v6e99gj5us"
assignmentId: "as_zbjw1l0cmp"
costUsd: 2.3149532
tokens: 115748
turns: 42
createdAt: "2026-11-04T18:23:32.854Z"
updatedAt: "2026-11-04T18:23:41.730Z"
---
## What I did
Measured what the hourly run misses, then built both of Mitchell's asks into the same backup worker. Draft PR https://github.com/mitchellgordon95/muster-town/pull/316 is open, and I'm parked on its CI.

## Findings
- **Measured live:**
  - Health shows `hosted.count` 2. /api/collectives lists hollyville and trauma, with 150 and 72 events. Neither has any transcript yet.
  - Workshop transcripts, summed from the "Transcript kept" events (`payload.storedBytes`) over all 117,782 events: 2,072 files, 233 MB stored (1.45 GB raw), largest 2.2 MB.
  - Growth is about 25 MB/day (range 7–65 MB/day from 10-27 to 11-04), which reaches about 2.3 GB at the 90-day retention. That is under the 2 GB bar today, so I shipped it rather than proposing a grant.
  - The desk has no flyctl, so I could not run `ls /data/hosted` on the box. The first live run's `backup.copies` will show which DBs it found.
- **PR #316:**
  - **Hosted DBs:** hub.db goes to `hosted/hub/<stamp>.db.gz.enc` and each `<slug>/data/town.db` to `hosted/<slug>/<stamp>.db.gz.enc`. They use the same copy, integrity_check, gzip, encrypt, verify-by-download and never-replace guard as town.db, with the same 48 hourly + 30 daily retention per prefix. The list is read from disk every run.
  - **Transcripts:** each `.jsonl.br` not yet in the bucket is encrypted only (it is already brotli) and uploaded once as `transcripts/<town>/<date>/<sessionId>.jsonl.br.enc`. Each upload is verified by download (sha256). Objects older than retention + 1 day are deleted. The first run uploads all 233 MB.
  - **Unchanged:** town.db's `town/` keys, restore.ts and the drill path.
  - **Failures:** a failed hosted copy or transcript upload goes into `backup.error`, prefixed with its prefix, so the monitor goes yellow. town.db's copy still counts when that happens.
  - **Fresh-town guard:** a fresh town.db still refuses the whole run.
  - **Health:** `backup` gains `copies` [{prefix, key, bytes}] and `transcripts` {files, uploaded, uploadedBytes, deleted}, stored in additive migration 090 (`backup_state.detail`).
  - **Restore tools:** restore-helper.mjs gains `list <prefix>` and `decrypt-raw`.
  - **Docs:** deploy/README.md "Backups" and "Recover" are rewritten.
- **Verified:** typecheck is clean. Server tests pass (283/283), including 4 new backup tests: sources, hosted copy + retention + transcript upload/prune, a failed hosted copy shown as the error, and the fresh-town guard. Core tests pass (727/727). The server build bundles the worker.
- **Known limit:** if a session's transcript is replaced later (a rare re-upload), the newer version is not uploaded again.
- **Next session:**
  1. Merge #316 on green, after checking that 089 is still the highest migration on main.
  2. Park on the merge sha.
  3. Check live `/api/health` `backup`: `copies` should list hosted/hub/, hosted/hollyville/ and hosted/trauma/, `transcripts.uploaded` should be about 2,072 on the first run, and `error` should be null.
  4. Rewrite topic page [dc_jyioru2ua3](../../wiki/2026-10/2026-10-31-backups-and-restore-ioru2ua3.md).
  5. Tell Pix (ag_mh0qidzgw6) a two-line answer for Mitchell.

## What I need from you
Nothing needed.
