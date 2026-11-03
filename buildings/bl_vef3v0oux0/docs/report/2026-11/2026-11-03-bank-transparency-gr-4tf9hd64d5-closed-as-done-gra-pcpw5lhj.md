---
id: "dc_50pcpw5lhj"
type: "report"
state: "building"
title: "Bank Transparency: gr_4tf9hd64d5 closed as done, grant pages now list their sessions (live at eff2251)"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_o58y0mjpkh"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "pending"
sessionId: "se_vb5m4w1223"
createdAt: "2026-11-03T03:22:28.423Z"
updatedAt: "2026-11-03T03:22:28.423Z"
---
Live: eff2251 (since 03:18 UTC; contains PR #276). This rollup is the close report for gr_4tf9hd64d5.

## Shipped

**1. Every grant page lists the sessions that spent its tokens**
**What it is:** Each grant's page now has a Sessions section: one row per session (date, agent, assignment, model, adjusted tokens, ≈ $ at API list price, and a link to its report or "error, no report"), with a footer that sums the rows and marks ✓ when the sum equals the grant's spent figure. The same data is at `GET /api/sessions?grantId=…`, and `npm run check:finance` now checks that every grant's sessions sum to its spent tokens (50 grants, 376 sessions, 20,349,087 adj. tokens, 33/33 checks pass). PR #276 (376301cc), grant gr_4tf9hd64d5, verified signed out by Nell 1 ([dc_o58y0mjpkh](2026-11-03-grant-sessions-section-verified-live-at-eff2251a-b-8y0mjpkh.md)).
**What you'd see:** `muster.town/workshop/?guest#/grant/gr_gmzli3f96j`, scroll to Sessions: 12 rows, footer "12 sessions · 698,207 adj. tokens = spent ✓ · ≈ $13.96 at API list price". For gr_iq5m7dug56 the API returns 19 sessions totalling 1,640,037 adj. tokens, equal to its spentTokens (≈ $36.79).
![Sessions section on a grant page](/api/media/mf_e2mhv0mkrk)
**Your call:** Mark kr_tqjylvupko and kr_o550w4u25b met or missed on gr_4tf9hd64d5 (closed as done: 177,688 of 200,000 tokens spent, 22,312 returned to the Bank). A one-line CSS fix (PR #279: the date column overlapped the title in 12-hour locales, visible as "AM" in the picture) merges on green CI on its own.

## Decided
- [dc_o58y0mjpkh](2026-11-03-grant-sessions-section-verified-live-at-eff2251a-b-8y0mjpkh.md) → approve (both key results verified live; grant closed; #279 continues on its parked continuation as_usrhxgujtm).

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_4tf9hd64d5 (grant pages list sessions, closed done) | kr_tqjylvupko: grant page shows its sessions with tokens and $ | claimed | 177,688 / 200,000 |
| gr_4tf9hd64d5 | kr_o550w4u25b: sessions sum to the grant's spentTokens, checked by check:finance | claimed | 177,688 / 200,000 |

No funded grant is open. Spend today by lane: exploration 0 tokens, directed 119 tokens; free under our goal 0 (held: as_ricjwkoaxc, the live check of the prompt-caching fix, waits for free tokens).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_lwgus14rd2), 0 requests, 3 rollups ([dc_4s6sdf5p6g](2026-11-02-bank-transparency-spending-tab-per-grant-lines-neg-6sdf5p6g.md), [dc_quybc4r5za](2026-11-03-bank-transparency-cost-estimate-step-2-live-overdr-ybc4r5za.md), [dc_3t9q4jcui1](2026-11-03-bank-transparency-gr-dt1l35tydx-closed-as-done-spe-9q4jcui1.md))._
