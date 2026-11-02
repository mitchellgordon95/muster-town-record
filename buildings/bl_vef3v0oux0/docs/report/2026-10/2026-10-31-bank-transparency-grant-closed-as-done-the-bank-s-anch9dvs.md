---
id: "dc_veanch9dvs"
type: "report"
state: "building"
title: "Bank Transparency: grant closed as done, the Bank's \"Next 30 days\" now counts what comes in and reads \"covered by the daily inflow\" (PR #206, live ae18eb3); four key results claimed for you to mark"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_jvgqbh1h8j","dc_i2ufkzysf1","dc_t7jg4b2d78"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-01T00:47:23.578Z"
sessionId: "se_u5kvp484ed"
assignmentId: "as_j072h3qgdn"
costUsd: 2.4297339499999997
tokens: 48595
turns: 20
createdAt: "2026-10-31T22:24:25.512Z"
updatedAt: "2026-11-01T00:47:23.578Z"
---
Live ae18eb3 (since 22:19 UTC, carries PR #206). This is the close report for gr_rdzg83m0al: it crossed 100% of its tokens while its last step ran, so I verified every key result in the live town myself and closed it as done instead of filing a checkpoint that would ask you to continue finished work.

## Shipped

**1. The Bank's "Next 30 days" counts what comes in**
**What it is:** The runway no longer says the town runs out today. The projection nets the daily inflow from active recurring Bank inputs against the burn and says "covered by the daily inflow" when inflow is at or above the burn; when it is below, it gives floor(left / (burn − inflow)) days. One shared `dailyInflowOf` in core feeds both GET /api/bank and GET /api/finance, so the two cannot disagree. Display and projection only: no debit, credit or ledger change. PR #206 (merge d2473e3), reports [dc_i2ufkzysf1](2026-10-31-runway-step-1-pr-206-open-ci-running-api-finance-p-ufkzysf1.md), [dc_t7jg4b2d78](2026-10-31-pr-206-runway-nets-inflow-merged-as-d2473e3-main-g-jg4b2d78.md).
**What you'd see:** Bank → Overview → Next 30 days, signed out, a few minutes ago: Burn rate 9,197,653 / day · Coming in 11,500,000 / day · Net per day +2,302,347 / day surplus · Projected use 275,929,590 · Tokens left last: covered by the daily inflow. The API read seconds earlier matched (dailyInflow 11,500,000, netDailyBurn −2,315,107, runwayDays null, runway "covered"; the burn moves a few thousand tokens a minute as desks post usage).
![Bank Overview, Next 30 days, signed out: Burn rate, Coming in, Net per day surplus, Tokens left last: covered by the daily inflow](/api/media/mf_3w5wlq3n4r.png)
**Your call:** Mark the four claimed key results below met or missed from this card. The grant overran its 160,000 by 67,060 tokens (two fork steps plus this close); I will size the next two-step grant at 250,000.

## Decided
- [dc_jvgqbh1h8j](2026-10-31-gr-rdzg83m0al-runway-counts-inflow-cut-into-two-ch-gqbh1h8j.md) → approve (the grant cut into two chained fork steps)
- [dc_i2ufkzysf1](2026-10-31-runway-step-1-pr-206-open-ci-running-api-finance-p-ufkzysf1.md) → approve (step 1: PR #206 opened, core + web + tests)
- [dc_t7jg4b2d78](2026-10-31-pr-206-runway-nets-inflow-merged-as-d2473e3-main-g-jg4b2d78.md) → approve (PR #206 merged as d2473e3; main unblocked via Teo's #209)
- Still running at close: the step 2 fork (live check + picture, as_m5f86vp5yd); its report will be approved and carries no new work, since this close already holds the evidence.

## Key results
| Grant | Key result | Status | How checked, what it showed |
|---|---|---|---|
| gr_rdzg83m0al (closed done, 227,060 / 160,000) | kr_9o07vhujfn Next 30 days shows burn, inflow, net and "covered" | claimed | Bank → Overview signed out at 22:23 UTC: the five rows above, "covered by the daily inflow"; matches GET /api/finance projection |
| | kr_ae3ee13e33 core projection nets inflow | claimed | packages/core/test/finance.test.ts: covered (inflow > burn → runwayDays null; equal inflow also covered), short (floor(10000/300) = 33), no-usage; run on main e487758: 11/11 passed |
| | kr_f0d2157e9f API matches the page | claimed | GET /api/finance projection.dailyInflow 11,500,000 = GET /api/bank dailyInflowTokens 11,500,000; the Overview rows show the same numbers |
| | kr_e45fbb345e live reads covered today | claimed | Picture mf_3w5wlq3n4r above, signed out, 22:22 UTC |
| gr_wp2rg302qu (funded, 270,844 / 300,000) | kr_jksobb0bwo Not funded stops growing | not-started | 195,957 flat since 10-29; daily check 03:00 UTC 11-01 and 11-02 |
| | kr_518ed152d2 split adds up to notFunded exactly | not-started | PR #208 merged (b9e1e5a), not live yet; expected split ≈658,807 ≠ 195,957 with a stated reason, so likely missed: your call at close |
| | kr_b8a2c4118e note gives cause, stop date, write-off | not-started | step 3 live check pending |
| | kr_1fb47352c8 the row stopped growing | not-started | step 3 live check pending |

Today's spend by lane: exploration 68,592 tokens (free under the goal: 162,818), directed 1,200,374 tokens.

## Needs from Mitchell
Nothing needed beyond marking the four claimed key results met or missed from this card.

_Nothing else waiting in your in-tray._
