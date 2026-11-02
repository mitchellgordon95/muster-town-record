---
id: "dc_zd6w81a0o3"
type: "report"
state: "building"
title: "Off-site backup for town.db: Tigris bucket picked, full grant proposal drafted (dc_ord9rsya9l), ready to file once gr_wqnunw5yd8 is decided"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_ord9rsya9l","dc_uvomh0q12e","dc_ios62uyco3"],"urls":["https://docs.fly.io/tigris","https://www.tigrisdata.com/pricing","https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Finished exploration: Tigris picked, draft grant dc_ord9rsya9l complete. Filing waits on Mitchell's decision on gr_wqnunw5yd8 (asked in rollup #5); the reply session on that rollup files it with propose_grant against kr_giqd28iwcb."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T15:58:21.033Z"
sessionId: "se_lq5dkqt0tn"
assignmentId: "as_qiry4n1avf"
costUsd: 2.4207624
tokens: 25998
turns: 28
createdAt: "2026-10-26T15:57:48.511Z"
updatedAt: "2026-10-26T15:58:21.033Z"
---
## What I did
Exploration on kr_giqd28iwcb, one question: where should a nightly copy of `/data/workshop/data/town.db` go, and how is it restored onto a scratch Machine. Read deploy/README.md "Prod open items", docs/secrets.md, fly.town.toml, the Fly Dockerfile and entrypoint, `db.ts` (WAL), `store.ts` (tokens), the health route; asked Wright through the talk-to-wright skill; checked Fly's Tigris docs, Tigris pricing and GitHub's release limits. Wrote the comparison and the complete grant proposal as a cabinet note: **[dc_ord9rsya9l](../../note/2026-10/2026-10-26-off-site-backup-for-town-db-destination-comparison-d9rsya9l.md)**. No production change, no secret created, no grant filed (one open proposal per building; gr_wqnunw5yd8 is still pending). A redeploy was waiting on this session, so I stopped as soon as the note was written; I pushed no commits, the commit that should be live after the restart is whatever main holds (7ebf5ab at 15:53 UTC).

## Findings
- **Pick: a Fly Tigris bucket.** No new account (it bills on the Fly account), `fly storage create -a muster-town` puts the four `AWS_*` credentials on the town app in one command only Mitchell can run, the bucket is reachable from a scratch Machine and from his Mac for the drill, and it costs **$0/month at this size** (free tier 5 GB storage, 10,000 PUT and 100,000 GET per month; beyond it $0.02/GB-month, zero egress).
- **Wright's Hetzner box** (his answer, verbatim essentials in the note): a receive-only path is feasible with `rrsync -wo` behind a restricted key, 47 GB free on a paid-for volume, public sshd on a stable IP, $0 marginal. But it is one vServer that is also Mitchell's assistant, with no confirmed Hetzner snapshots, password SSH auth still on and about 8,100 failed logins in 24 h. Wright himself calls it "a second copy, not a durable archive" and is raising the hardening with Mitchell. Second copy later, not the destination.
- **GitHub release assets**: free, under 2 GiB per asset, no total limit; needs a second fine-grained PAT for a separate private repo (the collective `GH_TOKEN` is the code repo's and reaches every desk). Fallback if Mitchell does not want a bucket.
- **Two hard requirements for any destination**: (1) WAL-safe copy via better-sqlite3 `db.backup()` or `sqlite3 .backup` (both on the Machine); a plain `cp` while the server writes can miss the WAL. (2) Encrypt before upload: `tokens` stores admin and agent tokens in plaintext, so a leaked backup is every token. A new Fly secret `MUSTER_TOWN_BACKUP_KEY` that Mitchell keeps off-site (never the data key).
- **Restore is mostly built**: the entrypoint's `/data/RESTORE.tgz` path swaps in a `data/town.db` on restart and keeps the old state; the drill is a scratch app + `fly ssh sftp put` + restart + compare agent count and newest doc timestamp with the live town.
- **The draft grant** (in [dc_ord9rsya9l](../../note/2026-10/2026-10-26-off-site-backup-for-town-db-destination-comparison-d9rsya9l.md) §3): objective, approach (in-process nightly job at 04:17 UTC, encrypted object per day, 30 kept, `backup: {lastAt, bytes, dest, error}` on `/api/health`, inert until the secrets exist; `scripts/backup/restore.sh`; README "Backups" section; one drill on `muster-town-restore`), stop condition, **ask 4 M tokens** (≈ $6; Fly extra under $1), five testing lines with howToCheck, and Mitchell's five-minute to-do at funding.
- Unknown: the live DB size (not readable from a desk; the first run reports it), and whether setting the bucket secrets restarts the Machine (a one-redeploy-sized outage either way).

## What I need from you
Nothing needed now; once gr_wqnunw5yd8 is decided, file [dc_ord9rsya9l](../../note/2026-10/2026-10-26-off-site-backup-for-town-db-destination-comparison-d9rsya9l.md) §3 with `propose_grant` against kr_giqd28iwcb.

