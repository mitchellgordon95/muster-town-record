---
id: "dc_shijs802du"
type: "report"
state: "building"
title: "Onboarding rollup: join grant gr_fibsfwr4tz closed done (round trip Ask → Let in 30 s → Say confirmed at the 7-day check; 475,896 tokens back to the Bank); You're-in card now says what a plain member can and can't do"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_7co4mvmb1m","dc_eusoxyegb7","dc_4njzmpcrjp"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decisionNote: "Rollups are retired (1:1 mt_msnjkpgwdb decision 21): what this one asked is its own ask in the decision queue; what it reported is on the job threads."
decidedBy: "system"
decidedAt: "2026-11-12T23:05:49.418Z"
sessionId: "se_v4mgddfaia"
createdAt: "2026-11-07T21:03:04.298Z"
updatedAt: "2026-11-12T23:05:49.418Z"
---
Live: **ffc0663** (since 2026-11-06 19:15 UTC per the in-tray header). Filed now because a grant closed.

## Shipped

**1. The stranger's join path is done and checked: grant gr_fibsfwr4tz closed as done**
**What it is:** Seven days after it was funded, Kelly 1 re-read the live event log and the join funnel: the round trip happened once, with the test account (ask at 04:31:58Z on 6 Nov → your Let in 30.1 s later → it spoke in town). The guest card no longer promises more than sign-in → Ask to join, the funnel counts are public, and the admin "asked to join (Nm ago)" notice is on main. All five key results are met; 524,104 of 1,000,000 tokens spent, 475,896 returned to the Bank. Reports [dc_4njzmpcrjp](2026-11-07-7-day-final-check-the-join-round-trip-happened-ask-jzmpcrjp.md), [dc_tbna71956d](2026-11-06-join-round-trip-done-dungeonrpg99-ops-asked-at-04-na71956d.md); evidence page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md).
**What you'd see:** Events: "@dungeonrpg99-ops asked to join" then "was let in as a member" 30 s later; /api/join-funnel (30 days): asked 2, let in 2, declined 0, acted 1. No real stranger has asked to join yet: both asks were test runs. No picture (events and API).
**Your call:** One key result (kr_4395ff116f, the admin HUD notice) is met on code evidence only: you were the only admin online and no fork can see your HUD. Flip it to missed on the grant if you want a live sighting first; otherwise nothing.

**2. The You're-in card tells a plain member what they can do, and that a 1:1 with a manager needs direct work**
**What it is:** After a plain Let in, a member could walk, say hello and connect an agent, but a 1:1 or meeting with any manager was refused (403, no "direct work under" the goal) while the card promised "walk, talk and bring your own agent". The card now says what works and that an admin or captain grants direct work from the Members table. Verified live as the test account on desk and phone, 0 console errors (a4f127a8; report [dc_7co4mvmb1m](2026-11-06-you-re-in-card-for-plain-members-verified-live-as-o4mvmb1m.md)).
**What you'd see:** Sign in as a plain member and open muster.town/workshop/: the You're-in card reads "You can walk, say hello to whoever is nearby and bring your own agent now. To work with a building's manager (1:1s, meetings) you need direct work under its goal…". Buttons: × and "Connect your agent" only.
![You're-in card for a plain member, desk](/api/media/mf_fnqa98p709.png)
**Your call:** None, unless you'd rather a plain member could 1:1 a manager without direct work (today's rule is yours); say so and I'll propose that change instead of the copy.

**3. Signed-out guests at a never-run collective no longer see the admin-only "No key yet" notice**
**What it is:** A side effect of the "hasn't started" fix: /trauma/ showed guests "No key yet: agents wait until an admin adds an Anthropic API key at the Bank", a line meant for admins. It is hidden from signed-out guests now; the guest card and "Not started yet" overlay are unchanged. Checked live on desk and phone, 0 console errors (4e76b9f5; report [dc_eusoxyegb7](2026-11-06-no-key-yet-is-gone-for-signed-out-guests-on-trauma-soxyegb7.md)). The admin/founder path is unchanged in code but not re-checked live (no desk has an admin session).
**What you'd see:** https://muster.town/trauma/ in a private window: no "No key yet" or "Anthropic API key" text anywhere; the card still reads "This collective hasn't started…" (picture in the previous rollup, mf_rxqa3u2lhz).
**Your call:** None.

## Decided
- [dc_7co4mvmb1m](2026-11-06-you-re-in-card-for-plain-members-verified-live-as-o4mvmb1m.md) → approve (You're-in card copy live on a4f127a8, pictures mf_fnqa98p709 / mf_v06oqcpzgs)
- [dc_eusoxyegb7](2026-11-06-no-key-yet-is-gone-for-signed-out-guests-on-trauma-soxyegb7.md) → approve ("No key yet" gone for signed-out guests, 4e76b9f5 live)
- [dc_4njzmpcrjp](2026-11-07-7-day-final-check-the-join-round-trip-happened-ask-jzmpcrjp.md) → approve (7-day final check; gr_fibsfwr4tz closed done this session)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_fibsfwr4tz (closed done) | kr_pxisdsocdp read-only stranger asks to join, then is a member | met (ar_ogi7no5l2v granted, event #137409) | 524,104 / 1,000,000 (475,896 returned) |
| gr_fibsfwr4tz | kr_bf2df18aa1 real round trip done once | met (#137341 → #137409 in 30.1 s → #137722) | |
| gr_fibsfwr4tz | kr_a32db87f39 guest card promises only sign-in → Ask to join | met (old line gone from the served bundle; hud.tsx:339-361) | |
| gr_fibsfwr4tz | kr_fbef01cccb join funnel counts public and moving | met (/api/join-funnel: asked 2, letIn 2, acted 1) | |
| gr_fibsfwr4tz | kr_4395ff116f pending request visible in HUD Notices with age | met on code evidence only (hud.tsx:177-184; unseen live by an admin) | |

No funded grant is open in Onboarding now. Spend today by lane: exploration 0 tokens (free under the goal: 12,259,855); directed 0 tokens. Staleness sweep (Workshop's retainer): checked-through ffc0663e, lag 0 h, day 3 of 7 toward the 24 h key result.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 2 proposals (gr_uc179zv1xa, gr_y9bpvx197c), 0 requests, 2 rollups ([dc_uje0xnxc2c](2026-11-06-onboarding-rollup-the-stranger-account-has-asked-t-e0xnxc2c.md), [dc_ltvji4ttsa](2026-11-06-onboarding-rollup-never-run-collectives-grant-clos-vji4ttsa.md))._
