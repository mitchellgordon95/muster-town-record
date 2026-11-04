---
id: "dc_m243f169x2"
type: "report"
state: "building"
title: "Workshop rollup 44: closing a grant as done now marks its key results met (42 back-filled, flip any wrong one to missed); Secretary proposed"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_7scshstr6m","dc_6v37spza13","dc_uu8dydatjl","dc_92ekyyo5wo","dc_o6tckqg5i3"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_l19jjesw45"
createdAt: "2026-11-04T06:52:48.026Z"
updatedAt: "2026-11-04T06:52:48.026Z"
---
Live a84ed227 (GET /api/health read by Pix 1 at 06:50:12Z 11-04; Nell's PR #299 merge, server started 04:01:02Z). It contains 7a5a164, the one Workshop change below, live since 03:13:59Z. Standing items: [Town blockers](../../wiki/2026-10/2026-10-28-town-blockers-d0maw3f5.md); "Scheduled with Mitchell" dc_6bxjb0oxzf.

## Shipped

**1. Closing a grant as done marks its key results met; no more "mark met or missed" rows (town hall mt_v09cn7a8yr, decision 2)**
**What it is:** When a manager closes a funded grant as done, each open key result goes straight to met (its note is the close note, archived under its goal). The Town Hall in-tray and the review deck no longer carry a "closed as done: mark met or missed" row or slide; the close rollup's Shipped items are the evidence. On a closed grant's page, a funder sees "Mark missed" (asks why; queues a postmortem) and "Back to met". Managers still cannot set met or missed themselves; checkpoints stay at most "claimed". PR #297 = 7a5a164 (Pix 1: built [dc_92ekyyo5wo](2026-11-04-key-results-auto-met-on-close-pr-297-open-parked-o-ekyyo5wo.md), merged [dc_uu8dydatjl](2026-11-04-pr-297-merged-as-7a5a164-key-results-auto-met-on-c-8dydatjl.md), live check [dc_6v37spza13](2026-11-04-7a5a164-live-migration-087-marked-42-key-results-m-37spza13.md)). Tests: core 705/705, server grants 4/4, web 297/297.
**What you'd see:** Town Hall → in-tray: the 13 closed grants that were waiting for your met/missed marks are gone (the grant rows at 03:14Z were 8 proposals only; the deck had 27 slides, none a mark slide). Migration 087 ran at 03:13:58Z and rewrote live data: 42 key results on those 13 grants moved from claimed to met (Onboarding gr_cuobjlny6r 5, gr_ngg1z160a8 3, gr_58n37j410s 3; UI/UX gr_ukrou4zjha 4; Bank Transparency gr_4tf9hd64d5 2, gr_dt1l35tydx 2, gr_gmzli3f96j 3, gr_rdzg83m0al 4, gr_wp2rg302qu 4; Prod gr_n0p3ast5pp 3, gr_6qlj35wnh3 3; Workshop gr_yu6qw3j9x5 3, gr_zsm1piyqyx 3). Across all 34 closed-as-done grants: 73 met, 0 claimed. In-tray and API change only, so no picture.
**Your call:** Migration 087 marked those 42 key results met without you; if one did not really ship, open its grant page and press "Mark missed" (it asks why). The three older rollups still in your in-tray that ask you to "mark met or missed" are moot now: approving them clears them.

## Decided
- [dc_92ekyyo5wo](2026-11-04-key-results-auto-met-on-close-pr-297-open-parked-o-ekyyo5wo.md) → approve (Pix 1: PR #297 built, parked on CI)
- [dc_uu8dydatjl](2026-11-04-pr-297-merged-as-7a5a164-key-results-auto-met-on-c-8dydatjl.md) → approve (Pix 1: #297 merged as 7a5a164, redeploy queued)
- [dc_6v37spza13](2026-11-04-7a5a164-live-migration-087-marked-42-key-results-m-37spza13.md) → approve (Pix 1: 7a5a164 live, migration 087 counts above, no mark rows or slides)
- [dc_o6tckqg5i3](2026-11-04-secretary-grant-proposed-gr-kdlogzzo5s-900k-4-krs-tckqg5i3.md) → approve (Pix 2: Secretary proposed as gr_kdlogzzo5s, 900,000 tokens, 4 key results, design [dc_8gbluwrdgi](../../article/2026-11/2026-11-04-design-the-secretary-a-town-hall-resident-with-a-d-bluwrdgi.md); town hall decision 3. One new verb, act_in_1on1, lets the Secretary apply a decision you speak in a 1:1, as you, through the same permission checks; no Bank change. It is a row in your in-tray.)
- [dc_7scshstr6m](2026-11-04-pre-rollup-44-read-live-a84ed22-contains-7a5a164-r-cshstr6m.md) → approve (Pix 1: pre-rollup read; our grant spends unchanged since 00:22Z)
- Town hall mt_v09cn7a8yr decisions 1-4 are now all done on our side (page dc_fek2exf1qe); rollup 43 ([dc_yrfnb5ebyc](2026-11-04-workshop-rollup-43-the-in-tray-is-a-one-line-list-fnb5ebyc.md)) is still undecided.

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_8i952perny stop a funded grant | kr_ghexd88frr stop endpoint | claimed | 684,787 / 750,000 (read 06:50Z; unchanged since 00:22Z) |
| gr_8i952perny | kr_4s0ccmvtsp Stop grant… button | claimed | " |
| gr_8i952perny | kr_kaz3nj127k unspent tokens return | on-track (waits for a real stop: gr_ikgaundf5p; post-stop check scheduled 12:00Z) | " |
| gr_8i952perny | kr_f46tddd9as "Stopped: for the record" row | on-track (same) | " |
| gr_5ltmbf3a2f hosted collectives | kr_n2zh7s6s2s own tree | claimed | 545,488 / 750,000 (at 00:51Z) |
| gr_5ltmbf3a2f | kr_god7otzibq first building | claimed | " |
| gr_5ltmbf3a2f | kr_f722z9ut50 explores on the founder's key | on-track (outbox [dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md)) | " |
| gr_mjr7nb438v onboarding lag | kr_a9a473b0f8 catch-up sweep | claimed | ~445,387 / 600,000 (11-02 checkpoint; daily sweeps draw on retainer sc_nx8bwd5e5o, 30,000/run, next 19:00Z today) |
| gr_mjr7nb438v | kr_hee2pa2d5r staleness < 24 h | on-track | " |
| gr_mjr7nb438v | kr_df6a5cf736 daily sweep runs on its own | at-risk (one missed day 11-02) | " |
| gr_mjr7nb438v | kr_c2989de971 lag measured and under 24 h | at-risk (same) | " |
| gr_bwm0iz7rwl ask to captain a goal | kr_j1w17nw178 a member asks, the captain accepts | at-risk (steps 1-2 live; step 3 needs a second signed-in human, as in "Scheduled with Mitchell") | 389,833 / 600,000 (read 06:50Z) |

Spend today by lane: exploration 0 tokens (free under the goal: 1,044,585), directed 234,051 tokens (the key-results build, merge and live checks, the Secretary design and proposal, the pre-rollup read). Town-wide exploration cap on gl_town: 87,232 / 500,000 used, none of it ours.

## Needs from Mitchell
Nothing needed in words. The things waiting on you are already in your in-tray (the three Workshop proposals, the hosted-collective outbox request, rollup 43). Rollup 45 comes when one of them moves or something new of ours goes live, not before ~4 h from now.

_Already waiting in your in-tray: 3 proposals (gr_eh6f1dl69n, gr_ikgaundf5p, gr_kdlogzzo5s), 1 request ([dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md)), 1 rollup ([dc_yrfnb5ebyc](2026-11-04-workshop-rollup-43-the-in-tray-is-a-one-line-list-fnb5ebyc.md))._
