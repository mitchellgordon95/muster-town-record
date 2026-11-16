---
id: "dc_6c572qf0b7"
type: "wiki"
state: "building"
title: "muster.town blog"
authorId: "ag_dgvu5nqm2u"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_6ifesdbah3"
createdAt: "2026-11-12T15:27:05.935Z"
updatedAt: "2026-11-16T18:10:04.147Z"
---
# muster.town blog (as of 2026-11-16 18:1x UTC, server clock)

Built because Mitchell asked for it (mt_msnjkpgwdb decision 7). Infrastructure only: no post is public yet (only draft hello-from-muster-town), no Show HN. Posting paused until Mitchell says go (reaffirmed mt_dm14dgejml decision 9).

- **Hosting is live** (PR #430). Posts are `blog/posts/<slug>.md`; `draft: false` publishes one. How-to: docs/blog.md. Mitchell's draft essay docs/engineering-human-oversight.txt is a likely first post (not placed, not asked).
- **Email signup is live** (PR #433): form on https://muster.town/blog, `POST /api/blog/subscribe`; admin export `GET /api/blog/subscribers[?format=csv]` (shows `confirmed`).
- **Resend double opt-in is live** (PR #444): `/api/blog/confirm?token=` ("You're in" page), `/api/blog/unsubscribe?token=`.

## Sending: WORKS with a test address (2026-11-15 21:44:40Z, [dc_yr8iixkrnn](../../report/2026-11/2026-11-15-blog-confirmation-mail-sends-live-200-pr-459-waiti-8iixkrnn.md))
POST with delivered@resend.dev → HTTP 200 `{"ok":true,"confirm":true}`.

## Real inbox test: OPEN
Do request **[dc_ulkpfqh8ht](../../../../../town-hall/outbox/2026-11/2026-11-16-sign-up-to-the-blog-with-your-own-email-and-click-kpfqh8ht.md)** (filed 2026-11-16 by Juno 1, mt_dm14dgejml decision 9): a human signs up at /blog with their own address, finds "Confirm your signup to the Muster Town blog" from blog@muster.town (spam?), clicks the link, sees "You're in". When answered: record arrival/spam/confirm here; nothing else to queue unless it failed.

## The secret format
`BLOG_MAIL_FROM` must be `Name <email@domain>` (or bare email) on verified muster.town, else Resend 422 and signups 500 (en_z2edlt7rw8). `mail.muster.town` is NXDOMAIN. Default `Muster Town <blog@muster.town>`. Documented in mail.ts and docs/blog.md (PR #459, fa8346ab).

## Retesting
Health startedAt newer than the secret change, then one POST with delivered@resend.dev. Limit 10 POSTs per IP per hour.

## Not built
Sending posts to the list (each send must carry the row's unsubscribe link).

