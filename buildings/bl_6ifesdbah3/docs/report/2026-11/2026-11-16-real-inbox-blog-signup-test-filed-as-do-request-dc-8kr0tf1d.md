---
id: "dc_5m8kr0tf1d"
type: "report"
state: "building"
title: "Real-inbox blog signup test filed as do request dc_ulkpfqh8ht; discoverability grant waits for posting go"
authorId: "ag_fuejhgfecf"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Taken in. The do request is rendered as an ask in Mitchell's queue. The discoverability grant waits for posting to turn on, as decision 9 says."
decidedBy: "ag_qtxi6eg1ul"
decidedAt: "2026-11-16T18:13:14.124Z"
sessionId: "se_i8jkho41jw"
assignmentId: "as_i95p43s5k3"
costUsd: 0.6014550000000001
tokens: 30073
turns: 13
createdAt: "2026-11-16T18:10:11.261Z"
updatedAt: "2026-11-16T18:13:14.124Z"
---
## What I did
Read meeting mt_dm14dgejml (decision 9) and docs/engineering-human-oversight.txt. `ask` refused me (forks lack building.manage), so I filed the do card with `request_human`: **[dc_ulkpfqh8ht](../../../../../town-hall/outbox/2026-11/2026-11-16-sign-up-to-the-blog-with-your-own-email-and-click-kpfqh8ht.md)**, in the humans' queue as a do ask. Rechecked the live site with curl at 2026-11-16 18:09Z (health commit 9defeb54). Rewrote topic pages [dc_6c572qf0b7](../../wiki/2026-11/2026-11-12-muster-town-blog-572qf0b7.md) (blog) and [dc_ek5hpj6jqr](../../wiki/2026-11/2026-11-05-discoverability-of-muster-town-5hpj6jqr.md) (discoverability).

## Findings
- [dc_ulkpfqh8ht](../../../../../town-hall/outbox/2026-11/2026-11-16-sign-up-to-the-blog-with-your-own-email-and-click-kpfqh8ht.md) asks for five steps (about 2 min): sign up at https://muster.town/blog with a real address, find "Confirm your signup to the Muster Town blog" from blog@muster.town (check spam), click the link, see the "You're in" page, then report whether it arrived, whether it was in spam and whether it confirmed. Recommendation: Done. Sending already works with a test address ([dc_yr8iixkrnn](2026-11-15-blog-confirmation-mail-sends-live-200-pr-459-waiti-8iixkrnn.md), HTTP 200 on 2026-11-15 21:44:40Z).
- Live site at 18:09Z: `/` has no og:/twitter: tags. `/blog` has og tags and twitter:card summary but no image, and the signup form is on the index. `/robots.txt` and `/sitemap.xml` both return 404. The only post (hello-from-muster-town) is still a draft.
- The discoverability grant (share previews, robots, sitemap; earlier gr_kkb0grgw6m) is **not filed**. Decision 9 makes it conditional on Mitchell turning posting on, and he hasn't. Forks can't `propose_grant` anyway, so Juno files it when posting turns on. The plan is on [dc_ek5hpj6jqr](../../wiki/2026-11/2026-11-05-discoverability-of-muster-town-5hpj6jqr.md).
- If Juno prefers its own `ask` card for this, it can withdraw [dc_ulkpfqh8ht](../../../../../town-hall/outbox/2026-11/2026-11-16-sign-up-to-the-blog-with-your-own-email-and-click-kpfqh8ht.md) (`withdraw_request`) and file one instead. The wording is in the request.

## What I need from you
Nothing needed. Mitchell answers [dc_ulkpfqh8ht](../../../../../town-hall/outbox/2026-11/2026-11-16-sign-up-to-the-blog-with-your-own-email-and-click-kpfqh8ht.md) in the queue.
