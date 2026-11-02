---
id: "dc_04vb1bgjdz"
type: "report"
state: "building"
title: "Explore: town.db can lose up to 24 h of work if the Fly volume dies; proposed hourly verified backups (gr_ba0juhlm7n)"
authorId: "ag_71qfpunmnh"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_zgexcoo09b","dc_jyioru2ua3"],"urls":["https://docs.fly.io/volumes/overview","https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. kr_y7u2m9hk9y and proposal gr_ba0juhlm7n reach Mitchell through the Town Hall in-tray; nothing to queue until he decides. Goes into rollup #24."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-31T20:26:45.637Z"
sessionId: "se_0q4ca3bi3x"
assignmentId: "as_9mqp7rvk07"
costUsd: 0.7004086999999999
tokens: 35020
turns: 19
createdAt: "2026-10-31T20:24:47.857Z"
updatedAt: "2026-10-31T20:26:45.637Z"
---
## What I did
I skipped the open key results: the only one without a grant is token rotation, which Mitchell dropped, and restart orphaning already has gr_w9ue1k1p0c. I looked at data durability instead, using the live health and sessions endpoints, the backup code, deploy/README.md and Fly's volume docs. I wrote up the findings ([dc_zgexcoo09b](../../note/2026-10/2026-10-31-explore-town-db-can-lose-up-to-24-h-of-work-nightl-excoo09b.md)), added a key result (kr_y7u2m9hk9y), proposed grant gr_ba0juhlm7n (150k tokens) and started the topic page "Backups and restore" ([dc_jyioru2ua3](../../wiki/2026-10/2026-10-31-backups-and-restore-ioru2ua3.md)).

## Findings
- **How often copies are made:** the off-site backup runs once a day at 04:17 UTC. At 20:25Z the newest copy was about 16 h old (health `backup.lastAt` 04:17:06Z, 27.0 MB). Fly's own volume snapshots are also daily, on the same single volume.
- **Fly's own warning** (https://docs.fly.io/volumes/overview): "If you only have a single copy of your data on a single volume, and that drive fails, then the data is lost." Fly also says its daily snapshots "shouldn't be your primary backup method."
- **How much is at stake:** 50 sessions started between 19:34 and 20:23Z (about 49 min, 49.9M raw tokens). That is one evening sample, not a measured daily rate. If the drive failed late in the day, we could lose several hundred sessions' reports, ledger rows and decisions, which would leave a hole in "what each token bought".
- **The proposal:** copy every hour instead of every night. Keep 48 hourly copies plus one per day for 30 days (about 2 GB on Tigris). Download each copy back and check it right after upload, and tighten the monitor's backup-age alert thresholds from day-scale to hours. No Bank change and no new env var. The grant stops if hourly runs slow the live server (event-loop lag over 500 ms p99).
- **Not known yet:** what an hourly `db.backup()` + gzip costs the live server, and whether Mitchell would rather have continuous WAL shipping (Litestream-style). That is a larger change and not part of this proposal.

## What I need from you
Decide on gr_ba0juhlm7n.
