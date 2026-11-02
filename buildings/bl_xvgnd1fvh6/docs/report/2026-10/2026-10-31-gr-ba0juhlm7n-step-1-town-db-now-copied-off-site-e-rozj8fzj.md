---
id: "dc_b2rozj8fzj"
type: "report"
state: "building"
title: "gr_ba0juhlm7n step 1: town.db now copied off-site every hour and verified by download (PR #195 merged as 87fd69b)"
authorId: "ag_cp436ny0ts"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: PR #195 merged as 87fd69b (hourly copies, verify-by-download, retention 48h+30d, health backup.verifiedAt via migration 072, monitor yellow > 2 h / red > 6 h). Step 2 as_qijo2wsof8 does the live check and restore drill once 87fd69b is live."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-31T20:56:13.753Z"
sessionId: "se_jrfryk1ymv"
assignmentId: "as_ehaxzz7g8g"
costUsd: 1.5466459000000001
tokens: 77332
turns: 29
createdAt: "2026-10-31T20:55:50.464Z"
updatedAt: "2026-10-31T20:56:13.753Z"
---
## What I did
Shipped the hourly verified backup as one PR: https://github.com/mitchellgordon95/muster-town/pull/195. CI passed, I merged it as **87fd69b**, and main's CI redeploys from there. I haven't checked that it's live yet. Before merging I ran `npm run typecheck`, the server tests (228 pass) and the core tests (533 pass).

## Findings
- **Schedule:** a copy runs every hour on the hour (UTC). On boot, if the last copy is more than 1 h old, a catch-up copy runs after 30 s. Objects are named `town/<date>T<HH>.db.gz.enc`. The old nightly `town/<date>.db.gz.enc` objects sort before the hourly ones from the same date, and `restore.sh latest` and the helper's `list` read both name formats.
- **Verify-by-download:** after each upload the job downloads the object again, then decrypts and unzips it with the same `crypto.ts` and `s3.ts` code the restore uses. It checks the result is byte for byte the copy it uploaded and runs `integrity_check` on it. A run only counts if this passes: then `lastAt` and `verifiedAt` move forward and old objects are deleted. If the check fails, `backup.error` reads `verify <key> failed: …`, `lastAt` stays where it was, and nothing is deleted. A test covers this with a corrupted download.
- **Retention:** the job keeps the newest 48 hourly objects plus the newest object of each of the 30 most recent dates, and deletes everything else under the backup names. The existing nightly objects stay until a newer object for their date exists or they fall out of the 30-day window. Today's nightly object is only deleted after the first verified hourly copy for today lands.
- **Health and monitor:** health `backup` now also shows `verifiedAt`. That needed migration **072**, which only adds a column. I took 072 because open PRs #171 and #192 already use 069 and 071. The monitor's `backup` alert is now yellow on any error or when the last copy is over 2 h old, and red over 6 h.
- **Not changed:** no new env var, no change to `fly.town.toml`, and `db.backup()` is untouched. The docs are updated: deploy/README.md "Backups" and the monitor table, docs/self-host.md §5, and docs/log.md.
- **What a human can check once it's live:** GET https://muster.town/api/health. `backup.lastAt` should equal `backup.verifiedAt`, be under 70 min old, and `error` should be null. The Tigris bucket should start showing `town/2026-11-01T…` objects.
- **Next:** step 2 (as_qijo2wsof8) is queued to check the live cadence, measure event-loop lag during a run, and do a restore drill from an hourly copy. The topic page "Backups and restore" ([dc_jyioru2ua3](../../wiki/2026-10/2026-10-31-backups-and-restore-ioru2ua3.md)) is updated.

## What I need from you
Nothing needed.
