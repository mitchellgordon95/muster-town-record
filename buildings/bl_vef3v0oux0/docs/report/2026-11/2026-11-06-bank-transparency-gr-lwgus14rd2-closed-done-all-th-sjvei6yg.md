---
id: "dc_j8sjvei6yg"
type: "report"
state: "building"
title: "Bank Transparency: gr_lwgus14rd2 closed done, all three key results live (manager wakes per building on Bank › Spending, the cache alert rebuilt around prefix busting and quiet in the HUD); 684,327 unspent tokens returned"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_o0b2tnnlpv","dc_2hvkqhb1j3","dc_626291r1xr","dc_8eo3hc0bgx","dc_asit591053","dc_3rupbiikz8","dc_ibnpman7xn","dc_sr6ldpani1","dc_h2mbpnwyjw"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/362","https://github.com/mitchellgordon95/muster-town/pull/364","https://github.com/mitchellgordon95/muster-town/pull/386","https://muster.town/api/finance/spend?window=7d","https://muster.town/api/events?alert=cache-miss&from=2026-11-06T00:00:00Z"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-06T17:16:21.230Z"
sessionId: "se_5z4lpnppkq"
createdAt: "2026-11-06T05:09:20.251Z"
updatedAt: "2026-11-06T17:16:21.230Z"
---
Live 1ea4b005 (since 2026-11-06 05:06 UTC; contains 5dc50c70, 41c5e7d7 and 1ea4b005). Grant gr_lwgus14rd2 closed as done at 05:08 UTC: 1,315,673 of the 2,000,000 tokens you set at 04:20 UTC spent, 684,327 returned to the Bank. The building has no funded grant now; gr_utygatbi85 waits in your in-tray.

## Shipped

**1. The Bank shows how often each building's manager woke, and what each wake and each decision cost (kr_avafh64h02)**
**What it is:** Bank › Spending › a building now has a "Manager wakes" table: one row per UTC day (newest 7) with wakes, adj. tokens, $, reports decided, cost per wake and per decision, plus a 7-day total; the sidebar Health box shows the town's 7-day wake count; /api/finance/spend returns `managerWakes`. PR #362, live as 41c5e7d7, verified against the API with check:finance 43/43 ([dc_sr6ldpani1](2026-11-06-manager-wakes-live-on-bank-spending-41c5e7d7-check-6ldpani1.md)).
**What you'd see:** https://muster.town/workshop/?guest#/bank › Spending › Bank Transparency › Manager wakes. Read at 04:51 UTC: town 965 wakes / $747.25 / 1,147 decided over 7 d; Bank Transparency today 6 wakes, $3.13, 9 decided (26,056 adj. tokens per wake); Town Workshop today 14 wakes, $14.89, 15 decided (53,191 per wake).
![Bank Transparency manager wakes per day](/api/media/mf_6111wzre43.png)
**Your call:** None

**2. The cache alert now measures prefix busting and the HUD shows only real ones; the false alarm is gone (kr_f49co6lg51)**
**What it is:** The old check fired on every healthy day (every cache write bills at the 1 h rate since 11-04). PR #364 (5dc50c70) replaces it: a purpose is flagged only when more than 10% of its sessions re-write most of their cached prefix on turns 2+, judged across the day after at least 5 ended sessions. PR #386 (1ea4b005) makes the HUD read the day's alerts from the server (`GET /api/events?alert=cache-miss&from=`) so an alert no longer drops out of the client's last-300-events window, and skips old share-format events. Verified live ([dc_2hvkqhb1j3](2026-11-06-5dc50c70-live-and-confirmed-the-only-cache-miss-al-vkqhb1j3.md), [dc_h2mbpnwyjw](2026-11-06-1ea4b005-is-live-the-cache-miss-alert-filter-works-mbpnwyjw.md)).
**What you'd see:** Signed out at https://muster.town/workshop/?guest, the HUD shows no "Cache alert" line. `GET https://muster.town/api/events?alert=cache-miss&from=2026-11-06T00:00:00Z` returns only the two pre-deploy share-format events (135616, 135623); nothing has fired since 04:19 UTC. API-only beyond that, no picture.
**Your call:** None

## Decided
- [dc_o0b2tnnlpv](2026-11-06-pr-364-cache-alert-keyed-on-prefix-busting-5-sessi-b2tnnlpv.md) → approved (PR #364 merged as 5dc50c70, parked on deploy)
- [dc_2hvkqhb1j3](2026-11-06-5dc50c70-live-and-confirmed-the-only-cache-miss-al-vkqhb1j3.md) → approved (5dc50c70 live, no false alert since the deploy, HUD quiet)
- [dc_626291r1xr](2026-11-06-grant-gr-lwgus14rd2-adjusted-2-000-000-tokens-6291r1xr.md) → approved (your adjust of gr_lwgus14rd2 to 2,000,000 taken in)
- [dc_8eo3hc0bgx](2026-11-06-pr-362-manager-wakes-brought-up-to-date-with-main-o3hc0bgx.md) → approved (PR #362 brought up to date with main, ready, parked on CI)
- [dc_asit591053](2026-11-06-pr-362-manager-wakes-merged-as-41c5e7d7-waiting-fo-it591053.md) → approved (PR #362 merged as 41c5e7d7, parked on deploy)
- [dc_3rupbiikz8](2026-11-06-hud-cache-alert-reads-the-day-s-alerts-from-the-se-upbiikz8.md) → approved (PR #386 HUD fix opened, parked on CI)
- [dc_ibnpman7xn](2026-11-06-pr-386-hud-cache-alert-merged-as-1ea4b005-parked-u-npman7xn.md) → approved (PR #386 merged as 1ea4b005, parked on deploy)
- [dc_sr6ldpani1](2026-11-06-manager-wakes-live-on-bank-spending-41c5e7d7-check-6ldpani1.md) → approved (41c5e7d7 live: manager wakes verified, check:finance 43/43)
- [dc_h2mbpnwyjw](2026-11-06-1ea4b005-is-live-the-cache-miss-alert-filter-works-mbpnwyjw.md) → approved; gr_lwgus14rd2 closed done with the evidence on [dc_qnpvanlfsb](../../wiki/2026-11/2026-11-04-token-cost-legible-gr-lwgus14rd2-plan-and-state-pvanlfsb.md)

## Key results
| Grant | Key result | Status | How to check | What the check showed | Spent / granted |
|---|---|---|---|---|---|
| gr_lwgus14rd2 (closed done) | kr_pzr1fkgas8 lane × token-kind table | met | Bank › Spending › By lane × token kind | Live since PR #315/#324, picture mf_464xs0edic | 1,315,673 / 2,000,000 |
| gr_lwgus14rd2 (closed done) | kr_f49co6lg51 cache-miss alert (prefix busting) | met | GET /api/events?alert=cache-miss&from=today; signed-out HUD | Only the 2 old share-format events; HUD quiet at 1400×900 | " |
| gr_lwgus14rd2 (closed done) | kr_avafh64h02 manager wakes per building | met | Bank › Spending › building › Manager wakes; managerWakes in /api/finance/spend | Rows match the API; check:finance 43/43; picture mf_6111wzre43 | " |

Spend today by lane: exploration 0 tokens; directed 309,311 tokens (the #364 merge and live check taken as directed work while the grant was held).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_utygatbi85), 0 requests, 0 rollups._
