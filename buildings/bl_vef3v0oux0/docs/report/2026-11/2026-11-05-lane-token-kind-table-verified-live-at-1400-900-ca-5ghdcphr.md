---
id: "dc_bl5ghdcphr"
type: "report"
state: "building"
title: "Lane × token-kind table verified live at 1400×900; cache-miss alert fires but the HUD never showed it, now being rebuilt around prefix busting (PR #364) with manager wakes per building (PR #362) close behind"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_uz526hq7x3","dc_mw7zg6516p","dc_lgh99v9tvd","dc_wozn4r2688","dc_7wrr65srdo"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-05T20:02:52.533Z"
sessionId: "se_jwwl3munnb"
createdAt: "2026-11-05T20:02:17.699Z"
updatedAt: "2026-11-05T20:02:52.533Z"
---
Live 62cf39f (since 19:45 UTC). Grant gr_lwgus14rd2 continued at 850,000 tokens (your +250k at 19:31 UTC); two PRs toward its last two key results are open and merge on green CI.

## Shipped

**1. The "By lane × token kind" table fits the Spending tab**
**What it is:** The Bank's Spending tab shows what each lane (grant, exploration, directed, retainer, manager) spent today and over 7 days, split by input, output, cache read and cache write. Its layout fix (5ad297d8, PR #324) is verified live: the summary columns stay left of the side panel and the per-kind columns scroll in their own box; folded, the tab fits one 1400×900 screen. check:finance passes 41/41 against live ([dc_mw7zg6516p](2026-11-05-gr-lwgus14rd2-step-1-done-lane-kind-layout-fix-5ad-7zg6516p.md)).
**What you'd see:** Bank → Spending → "By lane × token kind" → Show the table. Live 7 days (10-29 → 11-05 19:32Z): 2,180 sessions, 92.29M adj. tokens, ≈ $2,219, cache writes 54.0% of cost; manager lane 24.8M, $735, 67.2% cache writes.
![Lane × token kind at 1400×900](/api/media/mf_464xs0edic.png)
**Your call:** None

**2. The old cache-miss alert fires daily in the events log, but the HUD never shows it; it is being replaced**
**What it is:** The first alert (PR #326, 38c3e992) fires one `alert: cache-miss` system event per purpose per day at 1 h cache-write shares of 43–85%, often at 00:00–00:03Z on a single session. The HUD reads only the last 300 events, so the line scrolls out within minutes ([dc_lgh99v9tvd](2026-11-05-cache-miss-alert-pr-326-verified-live-in-the-event-h99v9tvd.md)). Per your redefinition, PR #364 (draft, CI finished) measures prefix busting instead: a session busts when most of its turns 2+ re-write ≥ 50% of their prefix; the alert fires when more than 10% of a purpose's day sessions bust, naming the worst ids. Live baseline on 37 of our sessions: 1–14% re-write per turn, max 20%, no session busts ([dc_7wrr65srdo](2026-11-05-cache-miss-alert-redefined-around-prefix-busting-p-rr65srdo.md)). The follow-up assignment (as_ail5blil47) merges it and makes the HUD read the day's alert from the server.
**What you'd see:** Nothing new live yet; API-only so far (GET /api/events shows the old events 122856–122860, 125905, 125954, 126027). The 1 h cache-write share stays a Spending column, without the red tint.
**Your call:** None

**3. Manager wakes per building per day (PR #362, open)**
**What it is:** A building's Spending level will list, per UTC day, how many times its manager woke, the adj. tokens and $, reports decided, cost per wake and per decision, with a 7-day total; the sidebar's Health box shows the town's 7-day wake count; /api/finance/spend returns `managerWakes` ([dc_wozn4r2688](2026-11-05-gr-lwgus14rd2-step-3-manager-wakes-per-building-pe-zn4r2688.md)). It covers the last 7 full days plus today regardless of the window switch. Full local check green; waits on CI, merges on green, no redeploy call.
**What you'd see:** Not live yet. After merge: Bank → Spending → a building → day lines "wakes / adj. tokens / $ / decided / per wake / per decision".
**Your call:** None

## Decided
- [dc_uz526hq7x3](2026-11-05-grant-gr-lwgus14rd2-adjusted-850-000-tokens-526hq7x3.md) → approve (grant continued at 850k; directed continuation as_0o6p2lgor6 cancelled, same work re-queued under the grant as as_ail5blil47)
- [dc_mw7zg6516p](2026-11-05-gr-lwgus14rd2-step-1-done-lane-kind-layout-fix-5ad-7zg6516p.md) → approve (kr_pzr1fkgas8 verified live)
- [dc_lgh99v9tvd](2026-11-05-cache-miss-alert-pr-326-verified-live-in-the-event-h99v9tvd.md) → approve (HUD window flaw folded into as_ail5blil47)
- [dc_wozn4r2688](2026-11-05-gr-lwgus14rd2-step-3-manager-wakes-per-building-pe-zn4r2688.md) → approve (its continuation as_hivj114a4v already queued)
- [dc_7wrr65srdo](2026-11-05-cache-miss-alert-redefined-around-prefix-busting-p-rr65srdo.md) → approve (continuation re-queued under the grant)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_lwgus14rd2 | kr_pzr1fkgas8 lane × kind table | claimed (verified live) | 734,638 / 850,000 |
| gr_lwgus14rd2 | kr_f49co6lg51 cache-miss alert (prefix busting) | on-track (PR #364) | " |
| gr_lwgus14rd2 | kr_avafh64h02 manager wakes per building | on-track (PR #362) | " |
| gr_qggxximtru | kr_au6pcldl3c | claimed | 456,488 / 450,000 (at checkpoint) |
| gr_qggxximtru | kr_ruh7apqptm "Paid in cash, last 30 days" | on-track (merged b39bfdaa, verify held) | " |

Spend today by lane: exploration 50,038 tokens; directed 186,013 tokens (the PR #364 session, before the grant was continued).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_utygatbi85), 0 requests, 0 rollups._
