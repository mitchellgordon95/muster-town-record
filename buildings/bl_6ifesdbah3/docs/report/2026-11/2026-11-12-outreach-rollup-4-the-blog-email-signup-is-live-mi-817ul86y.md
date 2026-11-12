---
id: "dc_cm817ul86y"
type: "report"
state: "building"
title: "Outreach rollup #4: the blog email signup is live; Mitchell's \"set up resend\" is queued and needs his Resend account and key"
authorId: "ag_qtxi6eg1ul"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":["dc_z3xtr8qluj","dc_3d8g7wfr01","dc_1gostt95ta","dc_xuzq6yphk6"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_o6bo862004"
createdAt: "2026-11-12T20:12:58.580Z"
updatedAt: "2026-11-12T20:12:58.580Z"
---
Live: 6e20eef since 2026-11-12 19:17 UTC. The signup commit 0a682c67 is in it.

## Shipped

**1. Every blog post now ends with an email signup**

**What it is:** The foot of each post and of the blog index has one email input, a "Sign up" button and the line "New posts by email. Nothing else." Addresses go into a mailing list table on the server. Only a signed-in admin can read the list, as JSON or CSV. There is no confirmation email and no unsubscribe link yet, because the town has no mail sender: that is the Resend work you asked for at 17:19 UTC, now queued (as_32xm8u4xiq). PR #433 (0a682c67); verified [dc_1gostt95ta](2026-11-12-blog-email-signup-is-live-the-only-thing-left-to-c-ostt95ta.md), re-checked [dc_xuzq6yphk6](2026-11-12-pre-rollup-check-blog-and-email-signup-are-still-l-zq6yphk6.md).

**What you'd see:** https://muster.town/blog and https://muster.town/blog/hello-from-muster-town show the form (the post itself is still a draft, so /blog says "No posts yet." and the Atom feed has 0 entries). A bad address gets "That doesn't look like an email address." A good one gets a 200 and lands in the list; our test row juno-verify-1794500532@example.com is there. Agents and non-admin users get 403 on the export. No picture: the form is three lines of plain HTML.

**Your call:** Open https://muster.town/api/blog/subscribers?format=csv while signed in and confirm you see the test row: that is the one path no agent can check.

## Decided
- [dc_z3xtr8qluj](2026-11-12-pr-433-ci-failed-on-knip-3-unused-exports-fixed-in-xtr8qluj.md) → approve (knip failure on PR #433 fixed; CI re-run)
- [dc_3d8g7wfr01](2026-11-12-email-signup-pr-433-merged-as-0a682c67-parked-unti-8g7wfr01.md) → approve (PR #433 merged as 0a682c67)
- [dc_1gostt95ta](2026-11-12-blog-email-signup-is-live-the-only-thing-left-to-c-ostt95ta.md) → approve (signup verified live; admin read left to Mitchell)
- [dc_xuzq6yphk6](2026-11-12-pre-rollup-check-blog-and-email-signup-are-still-l-zq6yphk6.md) → approve (pre-rollup check: still healthy at 6e20eef0)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| none funded | — | — | — |

Spend today by lane: exploration 0 tokens; directed 199,584 tokens (the four reports above plus the earlier blog-hosting work).

## Needs from Mitchell
1. Resend: create the account, verify a sending domain for muster.town and set the API key as a host secret on the live server. The ask card below has the steps. The code side is queued and will no-op until the key exists.
2. Open the subscriber CSV while signed in (the Your call above) and say whether the test row shows.

_Already waiting in your in-tray: 0 proposals, 0 requests, 2 rollups ([dc_e4k903km69](2026-11-05-outreach-rollup-2-the-repo-is-mit-licensed-pr-366-k903km69.md), [dc_uhli9tptwx](2026-11-12-outreach-rollup-3-blog-hosting-is-live-on-muster-t-li9tptwx.md))._
