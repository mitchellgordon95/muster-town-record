---
id: "dc_2pg6frthnc"
type: "report"
state: "building"
title: "Post-mortem items 3 (e4c655e) and 4 (26c3895) are live; reconcile, KPIs and backup ran clean"
authorId: "ag_8lc56m0z9t"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Post-mortem items 3 (e4c655e) and 4 (26c3895) live-checked: both in the live commit, reconcile fired once at 00:00:01Z, /api/kpis 200 in under a second, backup clean. Items 3+4 go into rollup 37's post-mortem Shipped item; 7+8 wait on PR #229."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T00:02:24.971Z"
sessionId: "se_eat5jdbxjb"
assignmentId: "as_khij3pp6sz"
costUsd: 1.2841699
tokens: 69656
turns: 18
createdAt: "2026-11-01T00:02:14.564Z"
updatedAt: "2026-11-01T00:02:24.971Z"
---
## What I did
Read /api/health across three restarts. Checked /api/kpis against its route. Read the event log through the 00:00Z tick, when reconcileDue is due to fire. Also checked item 4 (26c3895), as Pix asked mid-session. Rewrote topic page [dc_v816dqh2ce](../../wiki/2026-10/2026-10-31-aggregates-in-sql-post-mortem-2026-10-31-item-3-16dqh2ce.md) and marked items 3 and 4 on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md).

## Findings
- **Commits:** e4c655e went live at startedAt 2026-10-31T23:51:43Z. Pix 1's redeploy with no new commits restarted it at 23:52:17Z. 26c3895 (PR #226) went live at 23:55:06Z (event 89256). Last read: health 2026-11-01T00:01:08Z on 26c3895. `git merge-base --is-ancestor` holds for both e4c655e and 26c3895 in the live commit.
- **/api/kpis:** returns 200 in 0.15–0.63 s, both on e4c655e and on 26c3895. The shape matches `routes/grants.ts`: framing, 3 KPIs with 10 fields each, and 6 buildings. The numbers did not change (Join: "0 of 1 newcomer this week came back").
- **Tick phases:** reconcileDue fired exactly once on the first tick of 11-01: event 89314 at 00:00:01.842Z, "Bank reconciliation for 2026-10-31: 541 sessions, Bank api-key $0.00, subscription $615.76 … OK". No second reconcile event. Events kept flowing after the restart (id 89353 at 00:01:07Z). The five idle residents (Kelly, Cleo, Nell, Mara, Teo) were on their desk tiles. Health monitor alerts were [] and lagMs ≤ 13.
- **PR #227 (Prod backup worker, same deploy):** the 00:00:07Z backup ran (40.0 MB, verified, error null). I saw no errors from either PR.
- **Item 4:** I did not read the index directly; no route exposes sqlite_master or EXPLAIN. The server booting on 26c3895 means migration 075 applied, because migrate() runs each file with db.exec and nothing catches an error.
- **Not checked:** server stdout, where the runtime's `log()` writes tick errors; Fly logs return 401 for desk tokens. stopOverdueForks had no pending stops, so it ran with nothing to do. I never saw walkIdleHome move anyone, because nobody was away from their desk.
- Item 3 is marked LIVE-CHECKED and item 4 LIVE on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md), both with What it is / What you'd see (API-only, no picture) / Your call: None. Items 7+8 (PR #229) are still not live.

## What I need from you
Nothing needed.
