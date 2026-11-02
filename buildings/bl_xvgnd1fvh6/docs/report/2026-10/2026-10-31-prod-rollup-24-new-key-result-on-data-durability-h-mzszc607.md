---
id: "dc_qymzszc607"
type: "report"
state: "building"
title: "Prod rollup #24: new key result on data durability (hourly verified backups, proposal gr_ba0juhlm7n); gr_w9ue1k1p0c funded and its three steps queued"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_04vb1bgjdz","dc_asad3o5v4i"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T20:38:15.564Z"
sessionId: "se_6i4xpje4d1"
assignmentId: "as_e4u4i5fwr1"
createdAt: "2026-10-31T20:28:26.452Z"
updatedAt: "2026-10-31T20:38:15.564Z"
---
Live: e41f375 (other buildings' merges since #23: desk home-volume fork fix, Bank headline). Prod shipped nothing new since rollup #23 ([dc_tbl5ztn1lb](2026-10-31-prod-rollup-23-redeploys-have-cut-18-team-lead-ses-l5ztn1lb.md), ~35 min ago); this rollup is early because an exploration added a key result.

## Shipped
Nothing new from Prod since #23. Queued today under the grant you funded (gr_w9ue1k1p0c, 500k): step 1 as_yju5gyotox (sessions cut by a restart end as interrupted, not error, so the sessions alert stops firing on deploys), step 2 as_550a361mkl (manage sessions resume after a restart from their SDK session id; 8-minute drain with a wrap-up nudge; waits on step 1), step 3 schedule sc_ul1b1ntqik (daily 05:20Z check for 8 days from 11-02, report only). Each PR merges itself after CI green; they will show up as Shipped in the next rollup.

## Decided
- [dc_04vb1bgjdz](2026-10-31-explore-town-db-can-lose-up-to-24-h-of-work-if-the-vb1bgjdz.md) → approve. Finding ([dc_zgexcoo09b](../../note/2026-10/2026-10-31-explore-town-db-can-lose-up-to-24-h-of-work-nightl-excoo09b.md)): the off-site backup runs once a day at 04:17Z and Fly's own snapshot is also daily on the same single volume, so a volume failure late in the day loses up to ~24 h (one evening sample: 50 sessions in 49 min). New key result kr_y7u2m9hk9y (muster.town loses at most 1 h of state; hourly encrypted copies, each re-downloaded and checked). Proposal gr_ba0juhlm7n (150k) is in your in-tray.
- [dc_asad3o5v4i](2026-10-31-the-14-desk-errors-on-10-31-came-from-two-bugs-alr-ad3o5v4i.md) → approve (from #23's window): the 14 desk errors of 10-31 came from two bugs already fixed on main (interrupt-now 1cf60d4; frozen desk, PR #172), not from restarts, so gr_w9ue1k1p0c stays host-session only.

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_ohom5phapo redeploys no longer orphan team-lead work or page | gr_w9ue1k1p0c | not-started (steps 1-3 queued) | 0 / 500,000 |
| kr_og03nxrkct self-hosted towns directory | gr_8cdix9mpye | on-track (steps 1-2 live; step 3 deferred by you) | ~383,000 / 450,000 |
| kr_y7u2m9hk9y at most 1 h of state lost if the volume dies (new today) | gr_ba0juhlm7n proposed | not-started | 0 / 150,000 asked |

Today's spend by lane: exploration 141,010 tokens (free under the goal: 4,344,603), directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_ba0juhlm7n), 1 request ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), 0 rollups._

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_y7u2m9hk9y: "muster.town loses at most 1 hour of town state if its Fly volume dies: an encrypted off-site copy of town.db lands every hour, and a restore from the latest hourly copy is proven" (how to check: GET https://muster.town/api/health: backup.lastAt is never more than 70 min old over a day; the Tigris bucket lists hourly objects; deploy/README.md "Drill" records a restore of an hourly copy with MATCH; from [dc_zgexcoo09b](../../note/2026-10/2026-10-31-explore-town-db-can-lose-up-to-24-h-of-work-nightl-excoo09b.md))
