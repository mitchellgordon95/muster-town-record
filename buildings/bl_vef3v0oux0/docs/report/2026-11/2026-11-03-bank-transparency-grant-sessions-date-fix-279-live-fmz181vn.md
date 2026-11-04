---
id: "dc_qefmz181vn"
type: "report"
state: "building"
title: "Bank Transparency: grant Sessions date fix (#279) live and verified; prompt-caching fix cut warm manager wakes 42%; nothing funded open"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_63bwwb6kik","dc_wfctsms4zo","dc_meqatlild7"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/279","https://muster.town/workshop/?guest#/grant/gr_gmzli3f96j"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"1:1: Mitchell and Nell\": Bank UX pass as grant gr_567tikzitl (Nell, Bank Transparency): centered sheet with tabs · table · sidebar, Donate first with a chest fixture, active-only lists"
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-03T22:47:09.598Z"
sessionId: "se_vfe4zwv4yn"
createdAt: "2026-11-03T22:22:45.962Z"
updatedAt: "2026-11-03T22:47:09.598Z"
---
Live: 97a9570 (contains #279 as 02f1d1c, live since the 19:09Z redeploy).

## Shipped

**1. Grant page Sessions list: dates no longer overlap titles in 12-hour locales**
**What it is:** A CSS-only fix to the Sessions section of a grant page (PR #279, 02f1d1c): the date column is sized `max-content` with an 8 px gap, so an en-US date like "11-02 02:02 AM" no longer runs into the session title. Follow-up to the closed grant gr_4tf9hd64d5; cosmetic, not a key result. Verified signed out in headless Chromium with the locale forced to en-US ([dc_wfctsms4zo](2026-11-03-grant-sessions-date-column-fix-verified-live-at-ae-ctsms4zo.md)).
**What you'd see:** Open any grant page, e.g. `#/grant/gr_gmzli3f96j` as a guest: all 12 session rows render with the date cell ending at x 936 px and the title starting at x 944 px (before: mf_e2mhv0mkrk, titles overdrawn by "AM").
![Grant Sessions rows, dates clear of titles](/api/media/mf_fiwtgvel0z)
**Your call:** None.

**2. Prompt-caching fix (85498fa) measured live: warm manager wakes cost 42% less**
**What it is:** A measurement, not a change ([dc_meqatlild7](2026-11-03-prompt-caching-fix-holds-live-warm-manager-wakes-w-qatlild7.md), topic page [dc_qgl1lbe7wm](../../wiki/2026-11/2026-11-03-prompt-caching-fix-85498fa-measured-live-l1lbe7wm.md)). Across 6 managers' `manage` sessions before and after 85498fa went live: a warm wake (<60 min since the last) now writes a median 7,174 tokens to the 1-hour cache (was 22,448, range 17.7K–54.1K) and costs a median 24,205 adjusted tokens (was 41,680). Per manager the turn-1 write is flat at roughly its first message's size (Nell ~5.7K … Pix ~12.7K). Cold wakes (≥60 min) still write the whole prefix (~21–32K), as expected when the 1-hour cache has expired. What drives cost now is the 5-minute writes on long 12–28-turn wakes (31–42K), not the prefix. Caveat: the fork could not read manager transcripts (403), so it inferred turn-1 writes from each session's `cacheWrite1h`; post-fix sample is 29 warm and 6 cold wakes. API-only: no picture.
**What you'd see:** Spending tab or `/api/sessions?agentId=<manager>`: recent short manager wakes at ~10–25K adjusted tokens instead of ~40–50K.
**Your call:** None.

## Decided
- [dc_63bwwb6kik](2026-11-03-pr-279-merged-as-02f1d1c-grant-sessions-date-colum-bwwb6kik.md) → approve (PR #279 merged as 02f1d1c, redeploy queued; live check ran as as_geqr8309gz).
- [dc_wfctsms4zo](2026-11-03-grant-sessions-date-column-fix-verified-live-at-ae-ctsms4zo.md) → approve (fix verified live at ae3c4108; chain closed).
- [dc_meqatlild7](2026-11-03-prompt-caching-fix-holds-live-warm-manager-wakes-w-qatlild7.md) → approve (caching fix holds; no follow-up).

## Key results
No funded grant is open; the building queue is empty.

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_4tf9hd64d5 (closed done) | kr_tqjylvupko Sessions section on grant pages | claimed, awaiting your mark | 177,688 / 200,000 |
| gr_4tf9hd64d5 (closed done) | kr_o550w4u25b /api/sessions?grantId sums to spentTokens | claimed, awaiting your mark | 177,688 / 200,000 |
| gr_dt1l35tydx (closed done) | kr_f5gx4nuzuu, kr_d3mh9gmk2k Spending tab | claimed, awaiting your mark | 339,322 / 500,000 |
| gr_lwgus14rd2 (proposed) | kr_pzr1fkgas8, kr_f49co6lg51, kr_avafh64h02 token cost legible and watched | not started (awaiting funding decision) | 0 / 600,000 ask |

Spend today by lane: exploration 75,482 tokens (free under our goal: 4,137,222), directed 119 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_lwgus14rd2), 0 requests, 3 rollups ([dc_quybc4r5za](2026-11-03-bank-transparency-cost-estimate-step-2-live-overdr-ybc4r5za.md), [dc_3t9q4jcui1](2026-11-03-bank-transparency-gr-dt1l35tydx-closed-as-done-spe-9q4jcui1.md), [dc_50pcpw5lhj](2026-11-03-bank-transparency-gr-4tf9hd64d5-closed-as-done-gra-pcpw5lhj.md))._
