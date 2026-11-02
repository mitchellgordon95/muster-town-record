---
id: "dc_0j3slvx9nv"
type: "report"
state: "building"
title: "Bank Transparency: grant closed as done, the Bank now reads in dollars too (Overview, Spending) and a hosted collective's Hosting tab no longer counts the hub's machine (PRs #244, #253 live at b2b8789); three key results to mark; adjusted-token mix (#245) and the Not funded fix date (#221) also live"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_kca0g0guda","dc_og78q54rpo","dc_lponvvonpu","dc_h9t6jbpm85","dc_zhw01r640h","dc_1jjvze0ia2","dc_1fdng18cbd","dc_p9wjyrvzz9","dc_v88bqhpcdn","dc_9pznth69tm","dc_ye5lnjkx5b","dc_3cc2433rdt","dc_yt63799whm","dc_6lxlmf0sz6","dc_ng240psqf9","dc_z2r9tfg5zj","dc_mn2qlaylif","dc_nch68lb9vf"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/244","https://github.com/mitchellgordon95/muster-town/pull/253","https://github.com/mitchellgordon95/muster-town/pull/245","https://github.com/mitchellgordon95/muster-town/pull/221"]}
tags: ["rollup","checkpoint"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-02T02:29:00.208Z"
sessionId: "se_en151si4gp"
assignmentId: "as_bv0u7bilyj"
costUsd: 3.8431613499999995
tokens: 192158
turns: 48
createdAt: "2026-11-02T02:08:46.109Z"
updatedAt: "2026-11-02T02:29:00.208Z"
---
Live b2b8789 (since 2026-11-01 22:29 UTC; carries PRs #244, #245, #253 and #221). This is the close report for gr_gmzli3f96j: it crossed 100% of its tokens while its last step was waiting for the redeploy, so I did the live check myself in the checkpoint session, found all three key results true, and closed the grant as done. `npm run check:finance` against the live server: all 24 checks ✓ at 02:03 UTC.

## Shipped

**1. The Bank's Overview and Spending tabs show dollars next to tokens**
**What it is:** Every token figure that matters on the Bank's Overview (Used, Left, Burn per day, Coming in per day) and every building row on Spending now also reads "≈ $X", priced at Anthropic's API list price per session (each session at the list output price of the model its tokens are booked in: Opus 5.5 $20 per million, older Fable sessions $50 per million). One footnote says a subscription pays a flat fee instead. The server checks that the rows' dollars add up to the used dollars and prints a ✓ line. Display only: no stored figure, no charge, no migration. PR #244 (7c7b92b); GET /api/finance `usd` block and /api/finance/spend `usd` per row.
**What you'd see:** Signed out at muster.town/workshop/#/bank, Overview: "Used so far 84,694,657 ≈ $2,389.09", "Left 1,969,431 ≈ $39.39", "Burn rate 10,534,198 / day ≈ $210.68", "Coming in 1,428,571 / day ≈ $28.57", then "Dollars are at API list price; a subscription pays a flat fee instead." Spending: building rows $1,349.31 down to $4.85 and "✓ The server checked that the rows' dollars add up to the used dollars, $2,389.09 at API list price."
![Bank Overview: Used, Left, Burn and Coming in with their dollars at API list price](/api/media/mf_t1uwtl9c8f.png)
**Your call:** The grant's stop condition said to drop the dollars if you think list price misleads on a subscription-funded town. They are live now; say so if you want the "≈ $" removed (a small web-only change) or kept.

**2. A hosted collective's Hosting tab stops counting the hub's Town Machine as its own cost**
**What it is:** Before this, muster.town/hollyville's Hosting tab showed the hub's whole server Machine (about $32 over 30 days) as hollyville's cost. Now a hosted collective's /api/finance/fly returns townPaidBy "host" and townUsd 0, the window starts the day the collective was created, and the tab says the server is run by muster.town. The hub's own Hosting tab is unchanged (townPaidBy "self", Town Machine $31.99 over 30 days). PR #253 (26c2904).
**What you'd see:** Signed out at muster.town/hollyville/#/bank, Hosting: "The server is run by muster.town; this collective pays only for its own desks.", columns Desks / Total only, "Since it was created (2026-10-29 → 2026-11-02)", $0.00 (hollyville's desks are not on Fly).
![hollyville Hosting tab: the server is run by muster.town, desks only](/api/media/mf_kb6l6k1oe3.png)
**Your call:** None.

**3. The Tokens tab says what one adjusted token is made of, and the Not funded note states its fix date**
**What it is:** From your 1:1 ask (mt_rbc3exb393): one global mix, recomputed daily from the last 7 days of usage, on the Bank's "Tokens & sources" tab and in GET /api/finance and /api/bank as `mix`, with the weights formula and the cost shares. PR #245 (bf9bb3c). And from mt_p3ge56kg03: the Spending tab's "Not funded" note now names the date the leak stopped (2026-10-31, PR #131). PR #221 (416177f). Teo (UI / UX) has been told the mix block exists.
**What you'd see:** Signed out, Bank → Tokens & sources, under the inputs: "1 adj. token ≈ 30.4 raw tokens: 0.23% input, 94.8% cache read, 4.2% cache write, 0.74% output (from the last 7 days of usage, 1,652 sessions, updated daily; last 2026-11-02 00:00 UTC)" and "adj. tokens = output + 0.2 × input + 0.01 × cache read + 0.25 × cache write (5 min) + 0.4 × cache write (1 h) … Of what those tokens cost: 1.4% input, 28.8% cache read, 47.1% cache write, 22.7% output." No picture (two is the limit); the page text was read signed out.
**Your call:** None.

## Decided
- [dc_lponvvonpu](2026-11-01-dollars-on-the-bank-step-1-pr-244-conflicted-with-onvvonpu.md), [dc_h9t6jbpm85](2026-11-01-dollars-on-the-bank-step-1-pr-244-ci-failed-on-mai-t6jbpm85.md), [dc_zhw01r640h](2026-11-01-dollars-on-the-bank-step-1-pr-244-merged-as-7c7b92-w01r640h.md) (step 1, PR #244) → approve.
- [dc_1jjvze0ia2](2026-11-01-dollars-on-the-bank-step-2-hosted-hosting-tab-drop-jvze0ia2.md), [dc_1fdng18cbd](2026-11-01-dollars-on-the-bank-step-2-pr-253-merged-main-5f2c-dng18cbd.md), [dc_p9wjyrvzz9](2026-11-01-dollars-on-the-bank-step-2-pr-253-merged-as-26c290-wjyrvzz9.md) (step 2, PR #253) → approve.
- [dc_v88bqhpcdn](2026-11-01-dollars-on-the-bank-step-3-parked-until-26c2904-pr-8bqhpcdn.md) (step 3, parked; its resumption was held by the checkpoint) → approve; I did the live check in this session and cancelled the held step as_acltwk3k3v.
- [dc_9pznth69tm](2026-11-01-adjusted-token-mix-pr-245-fixed-deadcode-and-re-me-znth69tm.md), [dc_ye5lnjkx5b](2026-11-01-adjusted-token-mix-pr-245-ci-failed-on-main-s-own-5lnjkx5b.md), [dc_3cc2433rdt](2026-11-01-adjusted-token-mix-pr-245-ci-is-re-running-on-nell-c2433rdt.md), [dc_yt63799whm](2026-11-01-adjusted-token-mix-pr-245-went-conflicting-after-m-63799whm.md), [dc_6lxlmf0sz6](2026-11-01-adjusted-token-mix-pr-245-merged-as-bf9bb3c-mix-us-xlmf0sz6.md), [dc_ng240psqf9](2026-11-01-adjusted-token-mix-pr-245-merged-as-bf9bb3c-redepl-240psqf9.md) (PR #245 mix) → approve; the live check they asked for is done above, no new assignment.
- [dc_z2r9tfg5zj](2026-11-01-pr-221-not-funded-copy-still-open-main-merged-in-c-r9tfg5zj.md), [dc_mn2qlaylif](2026-11-01-pr-221-not-funded-copy-merged-as-416177f-redeploy-2qlaylif.md) (PR #221) → approve; the stale resumption as_qno3pcrexh cancelled.
- [dc_nch68lb9vf](2026-11-01-daily-check-bank-not-funded-flat-after-b44a0b8-kr-h68lb9vf.md) (daily Not funded reading 1 of 2: 195,957, flat) → approve; reading 2 fires at 03:00 UTC today.
- [dc_kca0g0guda](2026-11-01-gr-gmzli3f96j-dollars-on-the-bank-hosted-hosting-t-a0g0guda.md), [dc_og78q54rpo](2026-11-01-dollars-on-the-bank-step-1-pr-244-open-usd-at-api-78q54rpo.md) were approved earlier.

## Key results
Grant "Dollars on the Bank + hosted Hosting tab" (closed as done; the checkpoint fired at 506,049 / 500,000, 604,146 booked by the close: the sessions that merged main and re-ran CI on PRs #244 and #253 and this checkpoint session; 0 unspent).

| Key result | Status | How to check | What the check showed (02:03 UTC, b2b8789) |
|---|---|---|---|
| kr_ct7jyhctu7 Overview rows carry "≈ $X at API list price" + one footnote | claimed | Signed out, muster.town/workshop/#/bank Overview; GET /api/finance `usd` | Four rows carry $ (see item 1); usd {used 2389.09, left 39.39, burnPerDay 210.68, inflowPerDay 28.57}. Caveat: usd.used equals /spend usd.used to the cent, but it is the sessions' list-price sum ($2,411.04) less the Bank's own pricing difference ($18.03) and unfunded part ($3.92), so it is $21.95 under the plain sessions sum rather than "within $1"; the ✓ line holds within $0.02. |
| kr_xiwj6gon7n Spending rows carry $ and a ✓ line says they add up | claimed | Signed out, Bank → Spending; GET /api/finance/spend rows' usd, usdSumCheck | All 7 building rows show $; the ✓ dollars sentence is there; usdSumCheck ok, diff −0.02. |
| kr_cex3fn2g3t hollyville Hosting shows no Town Machine, says the server is run by muster.town | claimed | Signed out, muster.town/hollyville/#/bank → Hosting; GET /hollyville/api/finance/fly | Line shown, Desks/Total columns only, window since 2026-10-29; townPaidBy "host", townUsd 0, totalUsd 0. The hub still reads townPaidBy "self". |

No other grant is funded (gr_dt1l35tydx is proposed, your decision). Today's spend by lane: exploration 0 tokens (free under the goal: 0), directed 0 tokens.

## Needs from Mitchell
- Mark the three key results of the closed "Dollars on the Bank" grant met or missed from this report; the only caveat is the $21.95 reading on the first one, explained in the table.

_Already waiting in your in-tray: 1 proposal (gr_dt1l35tydx), 0 requests, 0 rollups._
