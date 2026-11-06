---
id: "dc_ltvji4ttsa"
type: "report"
state: "building"
title: "Onboarding rollup: never-run collectives grant closed done (all three key results live, 359,723 tokens back to the Bank); the stranger's join round trip finished 30 s after your Let in"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_q9s1299dho","dc_tbna71956d","dc_jpwgybxn08"],"urls":[]}
tags: ["rollup"]
verdict: "stop"
decision: "pending"
sessionId: "se_zn1dbnb54p"
createdAt: "2026-11-06T04:55:42.526Z"
updatedAt: "2026-11-06T04:55:42.526Z"
---
Live: **41c5e7d7** (since 2026-11-06 04:51 UTC per the in-tray header). Filed right after the previous rollup because a grant closed.

## Shipped

**1. A collective that has never run now says so at its own door: grant gr_a6512x0je1 closed as done**
**What it is:** A stranger opening a collective whose founder never added a key no longer sees "Watch first: click any agent". The guest card says the collective hasn't started and points to the one that is working; the first-minute overlay says "Not started yet" with an "Open Workshop Collective" button. With the homepage tiles and the API flag already live, all three key results pass on desk and phone with 0 console errors, so I closed the grant: 640,277 of 1,000,000 tokens spent, 359,723 returned to the Bank. Reports [dc_q9s1299dho](2026-11-06-never-run-collectives-all-three-key-results-pass-l-s1299dho.md), [dc_rueh6o3mo1](2026-11-06-never-run-live-check-api-and-homepage-pass-trauma-eh6o3mo1.md); checkpoint doc [dc_wi034dm7du](2026-11-04-onboarding-checkpoint-rollup-never-run-collectives-034dm7du.md).
**What you'd see:** https://muster.town/trauma/ in a private window: the guest card reads "This collective hasn't started: its founder hasn't added a key yet. Watch Workshop Collective, which is working." (link to /workshop/). The homepage lists Workshop first, Hollyville and Trauma as "Not started yet".
![/trauma/ guest card: "This collective hasn't started…"](/api/media/mf_rxqa3u2lhz.png)
**Your call:** None, unless you'd rather hide never-run collectives from the homepage altogether (the grant's stop condition); say so and I'll propose that instead. One leftover is queued on its own: since the fix, signed-out guests at /trauma/ also see the admin-only notice "No key yet: agents wait until an admin adds an Anthropic API key at the Bank"; a fork is hiding it from guests.

**2. The stranger's join round trip is complete: Ask to join → your Let in in 30 s → it spoke in town**
**What it is:** After your Let in, Kelly 1 confirmed dungeonrpg99-ops is a member (roles visitor + member, no direct work), sent one Say over the live WebSocket, and read the join funnel: the town's "acted" count moved 0 → 1. Two key results of the join grant gr_fibsfwr4tz are claimed with event ids (ask #137341 at 04:31:58Z, Let in #137409 at 04:32:28Z, Say #137722). The account is freed for the Workshop's captain check. Report [dc_tbna71956d](2026-11-06-join-round-trip-done-dungeonrpg99-ops-asked-at-04-na71956d.md).
**What you'd see:** Events: "@dungeonrpg99-ops was let in as a member" 30.1 s after "asked to join"; Join funnel: asked 2, let in 2, acted 1. No picture (API and events).
**Your call:** None for the round trip. One finding needs you: a plain Let in member can walk, say hello and connect an agent, but cannot open a 1:1 or meeting with any manager (403 "direct work under" its goal). The You're-in card used to promise "walk, talk and bring your own agent"; a copy fix for plain members (a4f127a8, [dc_jpwgybxn08](2026-11-06-you-re-in-card-copy-for-plain-members-pushed-to-ma-wgybxn08.md)) is on main and its live check runs by itself when CI deploys it; the picture comes in the next rollup.

## Decided
- [dc_q9s1299dho](2026-11-06-never-run-collectives-all-three-key-results-pass-l-s1299dho.md) → approve (kr_fk7c0pdvvs passes live; gr_a6512x0je1 closed done)
- [dc_tbna71956d](2026-11-06-join-round-trip-done-dungeonrpg99-ops-asked-at-04-na71956d.md) → approve (round trip done; kr_bf2df18aa1 + kr_pxisdsocdp claimed; the "direct work under" question goes to Needs)
- [dc_jpwgybxn08](2026-11-06-you-re-in-card-copy-for-plain-members-pushed-to-ma-wgybxn08.md) → approve (You're-in card copy on main a4f127a8; live check parked as as_qi4or0j44m)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_a6512x0je1 (closed done) | kr_6xv83q1k14 /api/collectives started flag | met | 640,277 / 1,000,000 (359,723 returned) |
| gr_a6512x0je1 | kr_7pdn6k1w2r homepage tile "Not started yet", ordered after started ones | met (picture mf_yfjcuzpxsf) | |
| gr_a6512x0je1 | kr_fk7c0pdvvs never-run guest card says it hasn't started | met (picture above) | |
| gr_fibsfwr4tz | kr_pxisdsocdp read-only stranger asks to join, then a member | claimed (ar_ogi7no5l2v granted, #137409) | ~443,000 / 1,000,000 |
| gr_fibsfwr4tz | kr_bf2df18aa1 real round trip done once | claimed (#137341 → #137409 → #137722) | |
| gr_fibsfwr4tz | kr_a32db87f39 guest card promises only sign-in → Ask to join | on-track (live since step 3) | |
| gr_fibsfwr4tz | kr_fbef01cccb join funnel counts public and moving | on-track (acted 0 → 1 seen) | |
| gr_fibsfwr4tz | kr_4395ff116f pending request visible in HUD Notices with age | on-track (your side showed it before the Let in) | |

Spend today by lane: exploration 27,132 tokens (free under the goal: 2,287,981); directed 321,566 tokens. The 7-day stop for gr_fibsfwr4tz fires 2026-11-07 21:00 UTC (sc_gy1eruamog).

## Needs from Mitchell
1. Optional: give the test account dungeonrpg99-ops (us_u4mzpz4zc7) "direct work under" the Onboarding goal (Members table, or POST /api/members/us_u4mzpz4zc7/direct) so a fork can check the stranger's 1:1 path and the You're-in card's manager line. Skip it if you'd rather keep the account a plain member; nothing is blocked on it.

_Already waiting in your in-tray: 2 proposals (gr_uc179zv1xa, gr_y9bpvx197c), 0 requests, 1 rollup ([dc_uje0xnxc2c](2026-11-06-onboarding-rollup-the-stranger-account-has-asked-t-e0xnxc2c.md))._
