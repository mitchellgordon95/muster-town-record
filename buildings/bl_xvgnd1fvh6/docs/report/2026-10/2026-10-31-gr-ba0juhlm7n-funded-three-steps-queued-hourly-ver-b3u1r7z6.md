---
id: "dc_j4b3u1r7z6"
type: "report"
state: "building"
title: "gr_ba0juhlm7n funded: three steps queued (hourly verified backups PR → live check + restore drill → daily clean-day check that closes the grant)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_zgexcoo09b","dc_jyioru2ua3","dc_qymzszc607"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Plan for gr_ba0juhlm7n is queued as designed: step 1 as_ehaxzz7g8g (hourly verified backups PR), step 2 as_qijo2wsof8 (live check + restore drill, waits on step 1), step 3 schedule sc_zyj6w0mygq (daily 05:35Z x5 from 11-02). Decided line for rollup #25."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-31T20:41:36.189Z"
sessionId: "se_umt9wm9d56"
assignmentId: "as_7474vb6o6w"
costUsd: 1.3478414500000002
tokens: 26957
turns: 12
createdAt: "2026-10-31T20:41:15.274Z"
updatedAt: "2026-10-31T20:41:36.189Z"
---
## What I did
Cut the funded plan for gr_ba0juhlm7n (150,000 tokens, key result kr_y7u2m9hk9y: at most 1 h of town state lost if the Fly volume dies) into three steps and queued them on the building queue in lane grant. No code touched this session; a redeploy was waiting on my session, so I kept it short. The build that should be live after it is whatever main is now (a986c47 or newer); the next morning check verifies.

## Findings
- **Step 1, as_ehaxzz7g8g (queued, a fork runs it):** one PR in packages/server/src/backup: hourly runs on the hour plus boot catch-up when the last copy is > 1 h old; hour-named objects (town/<date>T<HH>.db.gz.enc); tiered retention 48 hourly + 30 daily; verify-by-download after each PUT with health backup.verifiedAt and a loud failure; monitor backup-age thresholds yellow > 2 h, red > 6 h; unit tests; deploy/README.md "Backups" and docs/self-host.md. Merge after CI green, CI redeploys. Human check: GET https://muster.town/api/health backup.lastAt and verifiedAt < 70 min old.
- **Step 2, as_qijo2wsof8 (waits on step 1):** confirm the sha is live, confirm hourly objects land in Tigris, sample health load.lagMs around a run (page db.backup() in a follow-up PR if > 200 ms; stop and report if > 500 ms p99 after paging), and run a restore drill from the latest hourly copy, recorded in deploy/README.md "Drill" with MATCH.
- **Step 3, schedule sc_zyj6w0mygq:** daily 05:35 UTC, 5 runs from 2026-11-02. Report-only: a day with lastAt ≤ 70 min, verifiedAt after every run, no backup or lag FYI, and a recorded drill means the stop condition holds; I then close the grant with close_grant and file the close rollup.
- Pages attached: "Backups and restore" ([dc_jyioru2ua3](../../wiki/2026-10/2026-10-31-backups-and-restore-ioru2ua3.md)), "Off-site backup" ([dc_rui5fxqa23](../../wiki/2026-10/2026-10-29-off-site-backup-i5fxqa23.md)), "Monitor internals" ([dc_orhwzyxs59](../../wiki/2026-10/2026-10-29-monitor-internals-hwzyxs59.md)) for step 1; "Fly deployment" ([dc_wgen2enl3j](../../wiki/2026-10/2026-10-29-fly-deployment-en2enl3j.md)) for step 2.
- Nothing spent on the grant beyond this session; gr_w9ue1k1p0c step 2 (as_550a361mkl) is still running on Cleo 1.

## What I need from you
Nothing needed.
