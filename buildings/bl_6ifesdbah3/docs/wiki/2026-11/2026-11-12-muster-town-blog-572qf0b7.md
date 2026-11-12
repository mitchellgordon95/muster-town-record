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
updatedAt: "2026-11-12T20:20:15.847Z"
---
# muster.town blog (as of 2026-11-12 20:30 UTC)

Built on Mitchell's word (mt_msnjkpgwdb decision 7). Infrastructure only: no post is public yet, and there is no Show HN.

- **Hosting is live** (PR #430, 192ace07). Posts are `blog/posts/<slug>.md`. To publish one, set `draft: false`. The how-to is docs/blog.md. Verified in [dc_nlb86kmehq](../../report/2026-11/2026-11-12-blog-hosting-is-live-on-muster-town-blog-the-draft-b86kmehq.md).
- **Email signup is live** (PR #433, 0a682c67; verified in [dc_1gostt95ta](../../report/2026-11/2026-11-12-blog-email-signup-is-live-the-only-thing-left-to-c-ostt95ta.md)). `POST /api/blog/subscribe` adds an address. The admin export is `GET /api/blog/subscribers[?format=csv]`. Migration 112.
- **Resend double opt-in: PR #444 (4c6c5176), draft, open; not merged yet.** It adds `packages/server/src/mail.ts`, which calls Resend's HTTP API through fetch. It also adds migration 114 (`confirmedAt`, `confirmToken`, `unsubscribeToken`; existing rows are back-filled as confirmed) and three routes: `GET /api/blog/confirm?token=`, and `GET` and `POST /api/blog/unsubscribe?token=` with a List-Unsubscribe one-click header. The export gains a `confirmed` column. **It does nothing until the host secret `RESEND_API_KEY` is set.** Until then a signup stays single opt-in. The env is read at boot.

## What Mitchell does on Resend (read 2026-11-12)
1. Sign up at resend.com. **Free plan:** 3,000 emails/month, 100/day, 3 domains, 30-day retention (resend.com/pricing).
2. Go to Domains → Add `mail.muster.town`. Use a subdomain because Resend recommends one. Also, the root muster.town already has Namecheap email-forwarding MX records and an SPF record (`v=spf1 include:spf.efwd.registrar-servers.com`); a subdomain leaves them untouched. NS is Namecheap (dns1/dns2.registrar-servers.com). Copy the records from the domain's Records tab into Namecheap → Advanced DNS exactly as shown. Expect three of them: a DKIM TXT at `resend._domainkey.mail`, an MX at `send.mail` (the bounce Return-Path), and an SPF TXT at `send.mail`. Optional: a DMARC TXT at `_dmarc.mail`. Click Verify.
3. Go to API Keys → Create. Set Permission to **Sending access** and Domain to mail.muster.town.
4. Run `fly secrets set RESEND_API_KEY=re_… BLOG_MAIL_FROM="Muster Town <blog@mail.muster.town>" -a muster-town`. This restarts the Machine, so the server picks the values up. Prod reads host secrets from Fly secrets (deploy/README.md:22-23; docs/secrets.md:14).

## Once the key is set
A new signup gets the email "Confirm your signup to the Muster Town blog", and the form says "check your inbox". The link opens a "You're in" page. The unsubscribe link opens a "You're unsubscribed" page. The CSV shows `confirmed` yes or no.

Not built yet: sending posts to the list.
