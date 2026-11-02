---
id: "dc_inlbe2j84q"
type: "report"
state: "building"
title: "Bank Transparency: the Bank headline now says Claimed and Free (PR #180, live e41f375); stale-desk fix verified live; \"Not funded\" grant funded and step 1 queued"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_zxpcudyl9q","dc_3cuhr9j0we","dc_hlw8qinzwh","dc_2sr7r60qg5","dc_ngfjcoppjh"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/180"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T20:35:33.866Z"
sessionId: "se_2ajv5o7rqs"
createdAt: "2026-10-31T20:33:43.450Z"
updatedAt: "2026-10-31T20:35:33.866Z"
---
Live: e41f375 (since 20:26Z 2026-10-31), carrying PR #180.

## Shipped

**1. The Bank headline sub-numbers are now Claimed and Free**
**What it is:** Your flag asked for the sub-numbers under the Bank total to change from "expires today / permanent / held by buildings" to claimed and free. Done as a web-only change in all three places the headline appears: the marquee on the town map, the Bank flow view's title card and legend, and the Overview Balance table. Claimed = open reservations + open proposals' asks + funded grants' remaining; Free = the Bank's free tokens. A "Claimed" entry was added to the Terms block. No API or accounting change. ([dc_zxpcudyl9q](2026-10-31-bank-headline-now-shows-claimed-and-free-pr-180-li-pcudyl9q.md), flag [dc_md45lqrqvk](../../flag/2026-10/2026-10-31-nit-the-bank-headline-that-shows-how-many-tokens-a-45lqrqvk.md), PR #180, merged as 9fe1873)
**What you'd see:** Town map → the Bank marquee, or Bank → Overview → Balance table, signed out: total 5,945,737, CLAIMED 2,139,516, FREE 3,806,221. The old three rows are gone. The two sub-numbers add up to the total only while nothing is earmarked or held and free is above 0 (free is floored at 0).
![The Bank marquee: total 5,945,737, claimed 2,139,516, free 3,806,221](/api/media/mf_4gw8p7az7b.png)
**Your call:** None.

**2. Stale desks after an image redeploy: verified live**
**What it is:** The stale-desk path from the 1:1 (mt_cvxnqawx7h; PRs #139, #147 and Pix's #150) was checked live after the desk image rebuild. Four of six kept desks came back on the new image at once with staleDesk events; workshop-1, which was busy with Pix 1, came back four seconds after Pix 1 retired (event 68480, 02:12:18Z). At 06:00Z all six desk Machines were on the same image digest. ([dc_2sr7r60qg5](2026-10-31-stale-desks-verified-live-4-kept-desks-came-back-o-r7r60qg5.md), [dc_ngfjcoppjh](2026-10-31-workshop-1-came-back-on-the-new-desk-image-pr-147-fjcoppjh.md))
**What you'd see:** No UI change; operations only. The event log carries the staleDesk events and the desks all run the current image.
**Your call:** None.

## Decided
- [dc_zxpcudyl9q](2026-10-31-bank-headline-now-shows-claimed-and-free-pr-180-li-pcudyl9q.md) → approve (flag done, live and verified; Shipped item 1)
- [dc_3cuhr9j0we](2026-10-31-gr-wp2rg302qu-not-funded-row-explains-itself-cut-i-uhr9j0we.md) → approve (my plan for gr_wp2rg302qu: three steps; step 1 queued as as_wi2jzmuntc)
- [dc_hlw8qinzwh](2026-10-31-explore-not-funded-stopped-growing-at-195-957-prop-w8qinzwh.md) → approve (exploration on kr_jksobb0bwo: "Not funded" flat at 195,957 since 10-29; cause is the pre-PR #131 charge path that skipped the debit; it led to the proposal you funded)
- [dc_2sr7r60qg5](2026-10-31-stale-desks-verified-live-4-kept-desks-came-back-o-r7r60qg5.md) → approve (stale-desk live check, Shipped item 2)
- [dc_ngfjcoppjh](2026-10-31-workshop-1-came-back-on-the-new-desk-image-pr-147-fjcoppjh.md) → approve (workshop-1 came back on the new image, Shipped item 2)

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_jksobb0bwo "Not funded" row stops growing and explains itself | gr_wp2rg302qu | on-track: step 1 (per-building split in GET /api/finance/spend + tests) queued as as_wi2jzmuntc; step 2 (note copy) and 3 (live check, close) follow | 22,628 / 150,000 |
| kr_fydnpd8ok2 adjusted-token mix on the Tokens tab | none (your choice: no grant) | not-started; the one-shot directed check sc_p5oj6u7pks fires 2026-11-01 02:00Z | — |

Today's spend by lane: exploration 36,737 tokens (free under the goal: 3,746,407), directed 984,755 tokens. The daily check sc_qu4lpdmgng (03:00Z on 11-01 and 11-02) confirms "Not funded" stays at 195,957.

## Needs from Mitchell
Nothing needed.

_Nothing else waiting in your in-tray._
