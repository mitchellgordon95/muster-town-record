---
id: "dc_gmu7lw4u5h"
type: "report"
state: "building"
title: "Bank Transparency: the Finance page now lives on the Bank page (#/finance redirects to #/bank), verified live at f402bcf with UI/UX's tabs; 18/18 finance checks pass"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_c3v2nf1r05","dc_ocu8b5jry0","dc_i9u5zc26lm","dc_a3d7r97yby"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-30T19:17:13.097Z"
sessionId: "se_f58rk9u6jm"
createdAt: "2026-10-30T19:11:50.060Z"
updatedAt: "2026-10-30T19:17:13.097Z"
---
Live commit f402bcf (contains our 8305070 and Teo's tabs PR #119). All four key results stay met; nothing funded or proposed; building queue empty.

## Shipped

**1. One Bank page: the Finance page's sections moved onto the Bank page**
**What it is:** Your ask from the 1:1 with Cleo (mt_ew2d0mm7h9): no separate Finance page. Tokens, Next 30 days, Sources, Pool balances, Spending and Hosting (Fly.io) now render inside the Bank panel; the `finance` panel kind is gone, `#/finance` redirects to `#/bank`, and the HUD "$" opens the Bank. Commit 8305070 ([dc_i9u5zc26lm](2026-10-30-one-bank-page-mitchell-via-cleo-1-1-mt-ew2d0mm7h9-u5zc26lm.md)), verified live at f402bcf by a fork ([dc_a3d7r97yby](2026-10-30-one-bank-page-verified-live-at-f402bcf-with-teo-s-d7r97yby.md)). Teo's #119 landed on top and splits the Bank into five tabs (Overview, Tokens & sources, Pools, Spending, Hosting); our sections sit inside those tabs and read well, so no reordering was needed.
**What you'd see:** Open https://muster.town/workshop/#/finance signed out: the hash becomes #/bank and "The Bank" opens with five tabs. Live at 19:09Z: total received 80,729,370, used 47,748,760, expired 22,088,791, left 11,425,859, overdrawn 534,040 adj. tokens; Fly today $0.54, last 30 days $15.89. `npm run check:finance` 18/18 ✓ against the live API; every amount column ends at one right edge at 1400 px and 1000 px.
![The Bank page at f402bcf: title, five tabs, Balance rows](/api/media/mf_vvibm28z5i.png)
**Your call:** None. If you'd rather the finance tabs be ordered or named differently, say so and I'll queue it (tab layout itself is Teo's).

**2. Hosting (Fly.io) rows: amounts right-aligned**
**What it is:** The per-building Hosting rows had their amounts drifting left of the other sections' columns; 5b95c21 puts them on the shared `.spend-row` layout. Verified live ([dc_c3v2nf1r05](2026-10-30-hosting-row-alignment-fix-5b95c21-verified-live-pi-v2nf1r05.md), picture mf_vs13hiiuir).
**What you'd see:** Bank → Hosting tab: desks and town rows end at the same right edge as every other table. No API change.
**Your call:** None.

**3. Merge-rule copies updated to your 2026-10-30 revision**
**What it is:** Your reply to Prod rollup #20 dropped the "ask first for schema migrations" rule. The building's board FYI ([dc_57nuw740sc](../../fyi/2026-10/2026-10-27-merge-rules-for-bank-transparency-revised-2026-10-nuw740sc.md)) and deploy topic page ([dc_a0q82pir2r](../../wiki/2026-10/2026-10-29-deploy-ci-and-push-for-bank-transparency-q82pir2r.md)) now match the town-wide FYI [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md); Cleo was told ([dc_ocu8b5jry0](2026-10-30-merge-rule-copies-updated-to-mitchell-s-revision-s-u8b5jry0.md)). Docs only, no code.
**What you'd see:** Nothing in the UI; the Bank Transparency board FYI reads the same as the Town Hall's.
**Your call:** None.

## Decided
- [dc_c3v2nf1r05](2026-10-30-hosting-row-alignment-fix-5b95c21-verified-live-pi-v2nf1r05.md) → approve (5b95c21 Hosting alignment live, 18/18 ✓)
- [dc_ocu8b5jry0](2026-10-30-merge-rule-copies-updated-to-mitchell-s-revision-s-u8b5jry0.md) → approve (merge-rule copies updated; Fly endpoint re-verified at aa91c40)
- [dc_i9u5zc26lm](2026-10-30-one-bank-page-mitchell-via-cleo-1-1-mt-ew2d0mm7h9-u5zc26lm.md) → approve (one Bank page on main at 8305070)
- [dc_a3d7r97yby](2026-10-30-one-bank-page-verified-live-at-f402bcf-with-teo-s-d7r97yby.md) → approve (one Bank page verified live at f402bcf with tabs; picture mf_vvibm28z5i)

## Key results
| Key result | Status | Grant | Spent / granted |
|---|---|---|---|
| kr_j9058i256a Sources with amount, date, total | met | gr_gbpbbwy9b8 closed | closed, unspent returned |
| kr_97kyvac8f4 Pools and per-building allocation | met | gr_mijwhoiy2f closed | closed, unspent returned |
| kr_mx4odqn5xt Used, left, projection | met | gr_gi5jbgzv4k closed | closed, unspent returned |
| kr_q9oiu7a6ci Spending by building, grant, assignment | met | gr_8gtgmd828o closed | closed, unspent returned |

No funded grant. Today's spend by lane: exploration 0 / 828,571 tokens; directed 181,573 tokens (the one-Bank-page work and its live check, from your 1:1 via Cleo).

## Needs from Mitchell
Nothing needed.

_Nothing else waiting in your in-tray._
