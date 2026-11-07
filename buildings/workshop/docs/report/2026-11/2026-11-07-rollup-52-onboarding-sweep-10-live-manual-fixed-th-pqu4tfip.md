---
id: "dc_y3pqu4tfip"
type: "report"
state: "building"
title: "Rollup 52: onboarding sweep 10 live (manual fixed), the under-24 h streak broke at 24.06 h so sweeps go to every 12 h; test-account reset re-queued behind your captain accept"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_f6sk0z0znp","dc_ymwuryrav1","dc_2mfzdaj7qx"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_nlcubi92gy"
createdAt: "2026-11-07T05:25:39.983Z"
updatedAt: "2026-11-07T05:25:39.983Z"
---
Live: ffc0663 since 2026-11-06 19:15 UTC (sweep 10 of the onboarding-lag grant). Rollup 51 ([dc_hf4ziawngu](2026-11-06-rollup-51-the-stranger-test-account-is-in-asked-to-4ziawngu.md)) is still open in your in-tray; nothing in it has changed.

## Shipped

**1. The onboarding manual is current again (sweep 10), but the "every sweep under 24 h" streak broke by 4 minutes**

**What it is:** The daily sweep under grant gr_mjr7nb438v found two stale passages in the manual and fixed them (PR #393, merged as ffc0663). Lag is 0 h now, but at merge time it had reached 24.06 h, because yesterday's merge was 19:07Z and today's 19:10Z: with a daily fire, lag at merge equals the merge-to-merge interval, so a daily job can never stay reliably under 24 h. I moved the sweep to every 12 h (07:00Z and 19:00Z, 20k per run, until 11-14); that re-asks a 320k retainer, which is in your in-tray. Reports [dc_f6sk0z0znp](2026-11-06-onboarding-staleness-sweep-10-manual-fixed-pr-393-sk0z0znp.md), [dc_ymwuryrav1](2026-11-06-onboarding-sweep-10-merged-ffc0663e-lag-0-h-now-bu-wuryrav1.md).

**What you'd see:** The manual on muster.town reads correctly for the two passages sweep 10 touched; the Workshop schedule board shows "Onboarding staleness sweep" every 12 h, next 07:00Z today, held until the retainer is approved. Docs-only change: no picture.

**Your call:** Approve the 320k retainer so sweeps run twice a day and the streak restarts at day 1, or tell me to keep daily sweeps and accept that kr_hee2pa2d5r (every sweep under 24 h for 7 days) will be missed.

**2. The test account's first live reset is re-queued, still waiting on the captain accept**

**What it is:** The reset of dungeonrpg99-ops (POST /api/me/reset, live since PR #390) must run after the steer check, which waits on your accept of its ask to captain and on grant gr_bwm0iz7rwl at its checkpoint. The queued reset's 24 h wait expired with no cost; I re-queued it with the same guards (as_vvd2lycbnm), and it now also runs if you cut the grant instead. Notice [dc_2mfzdaj7qx](2026-11-07-pix-s-assignment-never-unblocked-first-live-reset-fzdaj7qx.md).

**What you'd see:** Town Hall in-tray: the "asks to captain" row for dungeonrpg99-ops (cr_6xfa4ka7bq) and the gr_bwm0iz7rwl checkpoint card, both unchanged since rollup 51. API-only: no picture.

**Your call:** None (the accept is the Needs line below).

## Decided
- [dc_f6sk0z0znp](2026-11-06-onboarding-staleness-sweep-10-manual-fixed-pr-393-sk0z0znp.md) → approve (sweep 10 PR #393 opened, parked on CI; decided 11-06 19:0xZ)
- [dc_ymwuryrav1](2026-11-06-onboarding-sweep-10-merged-ffc0663e-lag-0-h-now-bu-wuryrav1.md) → approve (PR #393 merged ffc0663, lag peaked 24.06 h, streak broke; decided 11-06 19:1xZ)
- [dc_2mfzdaj7qx](2026-11-07-pix-s-assignment-never-unblocked-first-live-reset-fzdaj7qx.md) → redirect (wait-expired reset re-queued as as_vvd2lycbnm with waitFor {assignment: as_krntgm6v02}, lane directed from mt_6kz0prkq8l)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_mjr7nb438v (onboarding lag) | kr_a9a473b0f8 catch-up sweep live | claimed | continued to 800,000 on 11-06; sweeps draw on the retainer, not the grant (schedules.ts:124) |
| gr_mjr7nb438v | kr_hee2pa2d5r every sweep under 24 h for 7 days | at-risk: streak broke day 3 (24.06 h), restarts 0 of 7 | same grant |
| gr_mjr7nb438v | kr_df6a5cf736 daily sweep runs on its own | on-track (10 sweeps) | same grant |
| gr_mjr7nb438v | kr_c2989de971 lag measured and under 24 h | on-track (0 h now) | same grant |
| gr_bwm0iz7rwl (ask to captain) | kr_j1w17nw178, kr_917dc5ba6d and the rest | at checkpoint; step 3 filed cr_6xfa4ka7bq, steer check held | held at checkpoint (card in your in-tray) |

Spend today (11-07, to 05:2xZ): exploration 0 tokens, directed 0 tokens; free under the Steer goal 12,067,083.

## Needs from Mitchell
- Accept dungeonrpg99-ops's ask to captain (the "asks to captain" row, cr_6xfa4ka7bq, in your in-tray): the steer check for kr_917dc5ba6d and the first live reset of the test account both wait on that one click.

_Already waiting in your in-tray: 1 proposal (gr_8bxoy2heif), 0 requests, 3 rollups ([dc_rvrpwohat5](2026-11-05-rollup-49-rename-and-retire-hosted-collectives-per-rpwohat5.md), [dc_430cifl3v5](2026-11-06-rollup-50-grants-a-b-c-and-the-throwaway-closed-1-0cifl3v5.md), [dc_hf4ziawngu](2026-11-06-rollup-51-the-stranger-test-account-is-in-asked-to-4ziawngu.md))._
