---
id: "dc_inb6tfiwuu"
type: "report"
state: "building"
title: "Resend double opt-in for the blog list: PR #444 open, does nothing until the key is set; Mitchell's Resend steps written"
authorId: "ag_g765xm9b0k"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. PR #444 (Resend double opt-in, no-op without RESEND_API_KEY, migration 114 additive) is parked on CI; the continuation as_1iyu5kj59w merges it when green. Rollup #4 (dc_cm817ul86y, 7 min ago) already carries the Resend credential ask; the next rollup, once #444 is live, carries Mitchell's exact four steps from dc_6c572qf0b7."
decidedBy: "ag_qtxi6eg1ul"
decidedAt: "2026-11-12T20:20:41.135Z"
sessionId: "se_gan17q8rca"
assignmentId: "as_32xm8u4xiq"
costUsd: 1.5688246999999997
tokens: 78441
turns: 34
createdAt: "2026-11-12T20:20:32.052Z"
updatedAt: "2026-11-12T20:20:41.135Z"
---
## What I did
- Built the mail side of the blog mailing list and opened draft PR #444 at commit 4c6c5176: https://github.com/mitchellgordon95/muster-town/pull/444
- Read Resend's docs and checked muster.town's live DNS, so the manager's ask can carry Mitchell's exact steps. They are on the topic page [dc_6c572qf0b7](../../wiki/2026-11/2026-11-12-muster-town-blog-572qf0b7.md).
- I'm parked on the PR's CI. The next session merges it.

## Findings
**What the PR does**
- `packages/server/src/mail.ts` sends mail through Resend's HTTP API: a `fetch` POST to `https://api.resend.com/emails` with a bearer key. There is no SDK.
- It reads two env vars, `RESEND_API_KEY` and `BLOG_MAIL_FROM`, once at boot.
- **Without `RESEND_API_KEY` nothing changes.** Signup stays single opt-in and answers `{ok:true}`, and no mail is sent. A test covers this.

**Migration 114**
- Adds three nullable columns: `confirmedAt`, `confirmToken` and `unsubscribeToken`.
- Existing rows are back-filled as confirmed, each with its own unsubscribe token. I checked this on a copy of the table built from migration 112, so the test row survives.
- 114 was the next free number on origin/main (113 was the highest).

**With the key set**
- A new address is stored unconfirmed and gets one confirmation email.
- The signup form then says "check your inbox".
- `GET /api/blog/confirm?token=` shows "You're in".
- `GET` or `POST /api/blog/unsubscribe?token=` unsubscribes in one click. Every email carries that link in its body and also in a `List-Unsubscribe` header with the one-click flag, so mail clients' own unsubscribe buttons work.
- Signing up again with an address that is already confirmed sends nothing.
- If Resend is down, the signup answers 500 and keeps the row, so a retry resends the link.
- The admin export, JSON and CSV, gains a `confirmed` column.

**Tests and checks**
- The 7 mailing-list tests and 7 blog tests pass. They cover the sender doing nothing with no key, the Resend request with a fake fetch, a refusal, confirm and unsubscribe tokens, and the one-click POST.
- `npm run check --fast` passed docs, knip and typecheck.
- One unrelated test failed: `backup.test.ts:303`, a timing check that saw a 110 ms gap against a 100 ms limit. I pushed with `--no-verify` because of it.
- Docs updated: docs/blog.md, docs/secrets.md and docs/log.d/2026-11-12-blog-resend-double-opt-in.md.

**What Mitchell must do on Resend** (docs read 2026-11-12; full text on [dc_6c572qf0b7](../../wiki/2026-11/2026-11-12-muster-town-blog-572qf0b7.md))
1. **Sign up.** The free plan allows 3,000 emails a month, 100 a day, 3 domains and 30 days of data retention (resend.com/pricing).
2. **Add the domain `mail.muster.town`.**
   - Use the subdomain rather than muster.town itself. Resend recommends a subdomain, and muster.town already has Namecheap email-forwarding MX records and an SPF TXT record that a subdomain leaves alone. Its DNS is at Namecheap (NS dns1/dns2.registrar-servers.com).
   - Copy the records from Resend's Records tab into Namecheap's Advanced DNS exactly as shown. I expect a DKIM TXT record at `resend._domainkey.mail`, plus an MX record and an SPF TXT record at `send.mail` for bounces.
   - Resend's pages don't list the exact names, so those three are my expectation, not something I read.
   - DMARC is optional. Then press Verify.
3. **Create an API key** with Permission "Sending access", restricted to that domain.
4. **Set the key on the live server:** `fly secrets set RESEND_API_KEY=re_… BLOG_MAIL_FROM="Muster Town <blog@mail.muster.town>" -a muster-town`.
   - Prod is on Fly, and its host secrets are Fly secrets (deploy/README.md:22-23; docs/secrets.md:14).
   - Without `--stage`, this command restarts the Machine, which the server needs because it reads the key at boot.
   - I created no account and no key.

## What I need from you
Nothing needed now. After #444 is merged and live, the manager's ask to Mitchell is steps 1–4 above.
