---
id: "dc_g2mdygebj5"
type: "report"
state: "building"
title: "Outreach rollup #5: Resend double opt-in is live and does nothing until Mitchell sets the key; his four steps are the ask"
authorId: "ag_qtxi6eg1ul"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":["dc_89vii5hy6m"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/444","https://muster.town/api/health"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_vtyjqygmzo"
createdAt: "2026-11-12T20:32:10.006Z"
updatedAt: "2026-11-12T20:32:10.006Z"
---
Live: 2f518b9 since 2026-11-12 20:29 UTC (PR #444). Filed 18 minutes after rollup #4 because you asked for a DO decision on Resend at 17:19 and the code is now blocked only on your key.

## Shipped

**1. The blog list now confirms signups by email and carries an unsubscribe link, once a Resend key exists**

**What it is:** The server has a mail sender that talks to Resend over HTTP. A new signup gets "Confirm your signup to the Muster Town blog" with a link; the email carries a one-click unsubscribe. Existing rows count as confirmed. With no key set, nothing changes: signup stays single opt-in and still answers ok. The subscriber export gains a `confirmed` column. PR #444 (2f518b9f); verified live in [dc_89vii5hy6m](2026-11-12-resend-double-opt-in-is-live-at-2f518b9f-with-no-k-vii5hy6m.md); your steps are on the building's "muster.town blog" topic page.

**What you'd see:** Today, nothing new on /blog: the form is the same, and a signup returns 200 with no email. The confirm and unsubscribe links answer 404 "That link didn't work" on a bad token. After you set the key, a signup shows "check your inbox", the link opens a "You're in" page, and https://muster.town/api/blog/subscribers?format=csv shows confirmed yes or no. No picture: the change is server routes and two plain HTML pages.

**Your call:** Do the four Resend steps (sign up, verify mail.muster.town in Namecheap DNS, create a sending-only key, `fly secrets set RESEND_API_KEY=… BLOG_MAIL_FROM="Muster Town <blog@mail.muster.town>" -a muster-town`) and tell me when it is set, or say not now and signup stays single opt-in.

## Decided
- [dc_89vii5hy6m](2026-11-12-resend-double-opt-in-is-live-at-2f518b9f-with-no-k-vii5hy6m.md) → approve (PR #444 live at 2f518b9f; signup unchanged without the key; confirm, unsubscribe and export answer as designed)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| none funded | — | — | — |

Spend today by lane: exploration 0 tokens; directed 318,504 tokens (the Resend build, merge and verify sessions plus the earlier blog work).

## Needs from Mitchell
1. Resend: sign up, add and verify the domain mail.muster.town in Namecheap, create an API key with sending access only, and set RESEND_API_KEY and BLOG_MAIL_FROM as Fly secrets on muster-town. The exact DNS records and the command are on the Outreach topic page "muster.town blog". Tell me when it is set and I will queue a live check of the confirmation email.

_Already waiting in your in-tray: 0 proposals, 0 requests, 3 rollups ([dc_e4k903km69](2026-11-05-outreach-rollup-2-the-repo-is-mit-licensed-pr-366-k903km69.md), [dc_uhli9tptwx](2026-11-12-outreach-rollup-3-blog-hosting-is-live-on-muster-t-li9tptwx.md), [dc_cm817ul86y](2026-11-12-outreach-rollup-4-the-blog-email-signup-is-live-mi-817ul86y.md))._
