---
id: "dc_yrfnb5ebyc"
type: "report"
state: "building"
title: "Workshop rollup 43: the in-tray is a one-line list you click into (your flag); hosted step 3 live; both continued grants now wait on you"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_3rpgs0bi1z","dc_pnl1061lu4","dc_2y9c6ucd6z","dc_tqu4xh9hgf","dc_v5zob62q6p","dc_m3ew6l74iy","dc_9xolx7w9x5","dc_3tkcch4qe7"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_jofuqbqvr3"
createdAt: "2026-11-04T02:46:53.563Z"
updatedAt: "2026-11-04T02:46:53.563Z"
---
Live 7e439b3f (GET /api/health read by Pix 3 at 02:44:54Z 11-04, server started 02:23:28Z). Both items below are in it. Standing items: [Town blockers](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md); "Scheduled with Mitchell" dc_6bxjb0oxzf.

## Shipped

**1. The in-tray is a one-line list you click into (your flag [dc_2hllscunfx](../../flag/2026-11/2026-11-03-can-you-make-the-intray-more-human-useable-i-m-thi-llscunfx.md))**
**What it is:** Every in-tray (Town Hall and each building) now shows each item on one line: building tag or author, truncated title (full title on hover), one pill (rollup / ⚑ flag / verdict / "asks 4M" / "2M / 2M" / "stopped · …") and time-ago; clicking a report line opens it with the review controls, other lines open their full row. A List / Cards toggle sits beside "Review as deck"; List is the default and your choice is remembered in the browser. PR #286 = 2eb0aac (Pix 1: [dc_pnl1061lu4](2026-11-03-in-tray-as-a-list-flag-dc-2hllscunfx-pr-286-open-p-l1061lu4.md), [dc_2y9c6ucd6z](2026-11-03-in-tray-list-flag-dc-2hllscunfx-pr-286-merged-as-2-9c6ucd6z.md), [dc_tqu4xh9hgf](2026-11-03-in-tray-list-flag-dc-2hllscunfx-is-live-on-2eb0aac-u4xh9hgf.md)); re-checked live on 7e439b3f by Pix 3 ([dc_3rpgs0bi1z](2026-11-04-in-tray-list-view-flag-dc-2hllscunfx-still-live-on-pgs0bi1z.md)): web tests 4/4.
**What you'd see:** Town Hall → in-tray: 40 items waiting as a guest at 02:44Z (21 manager reports, 19 grants: 13 closed awaiting your met/missed marks, 6 proposed), each on one line; the "Review as deck" button has List / Cards next to it.
![Town Hall in-tray, Manager reports in List mode](/api/media/mf_rp46hftazf)
**Your call:** List is the default for guests too (a bit beyond your "signed-in human" ask); say if Cards should stay the guest default.

**2. Hosted collectives step 3 is live: a founder's keyed collective explores on its own (gr_5ltmbf3a2f, kr_f722z9ut50)**
**What it is:** The last step of the hosted-collective grant: a new collective with a key credit starts exploration and files its first proposal without anyone touching it. PR #252 = 6051a41 (test + docs only; the behaviour was already in the server) is live, and the hub-explore test passes 2/2 on main (Pix 1: [dc_v5zob62q6p](2026-11-04-gr-5ltmbf3a2f-outbox-request-dc-31vt101dbe-filed-f-zob62q6p.md), [dc_m3ew6l74iy](2026-11-04-gr-5ltmbf3a2f-252-6051a41-is-live-hub-explore-2-2-ew6l74iy.md)). API-only, so no picture. You continued the grant at 750,000 at 00:51Z (545,488 spent then; [dc_3tkcch4qe7](2026-11-04-grant-gr-5ltmbf3a2f-adjusted-750-000-tokens-kcch4qe7.md)). The grant closes on your answer to outbox request [dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md) (a 5-10 min throwaway keyed collective).
**What you'd see:** Nothing new in the UI until the outbox check: after it, a throwaway collective's Workshop files a proposal into its in-tray and one Bank session appears on your key.
**Your call:** None (the outbox request carries it).

## Decided
- [dc_pnl1061lu4](2026-11-03-in-tray-as-a-list-flag-dc-2hllscunfx-pr-286-open-p-l1061lu4.md) → approve (Pix 1: PR #286 built, List view)
- [dc_2y9c6ucd6z](2026-11-03-in-tray-list-flag-dc-2hllscunfx-pr-286-merged-as-2-9c6ucd6z.md) → approve (Pix 1: #286 merged as 2eb0aac)
- [dc_tqu4xh9hgf](2026-11-03-in-tray-list-flag-dc-2hllscunfx-is-live-on-2eb0aac-u4xh9hgf.md) → approve (Pix 1: 2eb0aac live 22:54:17Z 11-03)
- [dc_3rpgs0bi1z](2026-11-04-in-tray-list-view-flag-dc-2hllscunfx-still-live-on-pgs0bi1z.md) → approve (Pix 3: List view still live on 7e439b3f, tests 4/4)
- [dc_v5zob62q6p](2026-11-04-gr-5ltmbf3a2f-outbox-request-dc-31vt101dbe-filed-f-zob62q6p.md) → approve (Pix 1: outbox request [dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md) filed for the keyed live check)
- [dc_m3ew6l74iy](2026-11-04-gr-5ltmbf3a2f-252-6051a41-is-live-hub-explore-2-2-ew6l74iy.md) → approve (Pix 1: #252 = 6051a41 live, hub-explore 2/2)
- [dc_9xolx7w9x5](2026-11-04-grant-gr-8i952perny-adjusted-750-000-tokens-olx7w9x5.md) → approve (town: gr_8i952perny continued at 750,000, 00:22Z)
- [dc_3tkcch4qe7](2026-11-04-grant-gr-5ltmbf3a2f-adjusted-750-000-tokens-kcch4qe7.md) → approve (town: gr_5ltmbf3a2f continued at 750,000, 00:51Z)
- Town hall mt_v09cn7a8yr (00:11-00:20Z, page dc_fek2exf1qe): decision 2 (key results auto-met on close) is being built by Pix 1 (as_mygyiflb6n); decision 3 (Secretary resident) is being written up and proposed by Pix 2 (as_cj1pde5t3n). Both land in rollup 44.

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_8i952perny stop a funded grant | kr_ghexd88frr stop endpoint | claimed | 684,787 / 750,000 (at 00:22Z) |
| gr_8i952perny | kr_4s0ccmvtsp Stop grant… button | claimed | " |
| gr_8i952perny | kr_kaz3nj127k unspent tokens return | on-track (waits for a real stop: gr_ikgaundf5p) | " |
| gr_8i952perny | kr_f46tddd9as "Stopped: for the record" row | on-track (same) | " |
| gr_5ltmbf3a2f hosted collectives | kr_n2zh7s6s2s own tree | claimed | 545,488 / 750,000 (at 00:51Z) |
| gr_5ltmbf3a2f | kr_god7otzibq first building | claimed | " |
| gr_5ltmbf3a2f | kr_f722z9ut50 explores on the founder's key | on-track (outbox [dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md)) | " |
| gr_mjr7nb438v onboarding lag | kr_a9a473b0f8 catch-up sweep | claimed | ~445,387 / 600,000 (11-02 checkpoint; daily sweeps now draw on retainer sc_nx8bwd5e5o, 30,000/run, next 19:00Z today) |
| gr_mjr7nb438v | kr_hee2pa2d5r staleness < 24 h | on-track (lag 0 h after sweep 7) | " |
| gr_mjr7nb438v | kr_df6a5cf736 daily sweep runs on its own | at-risk (one missed day 11-02) | " |
| gr_mjr7nb438v | kr_c2989de971 lag measured and under 24 h | at-risk (same) | " |

Spend today by lane: exploration 0 tokens (free under the goal: 2,410,535), directed 0 tokens.

## Needs from Mitchell
Nothing needed in words: the two things waiting on you are already in your in-tray (the throwaway stop-grant proposal and the hosted-collective outbox request). Rollup 44 comes when key-results-auto-met-on-close or the Secretary proposal lands, not before ~4 h from now.

_Already waiting in your in-tray: 3 proposals (gr_eh6f1dl69n, gr_ikgaundf5p, gr_kdlogzzo5s), 1 request ([dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md)), 0 rollups._
