---
id: "dc_4t9rqqh4kf"
type: "report"
state: "building"
title: "Resend key is seen live, but Resend rejects the send: BLOG_MAIL_FROM likely names an unverified domain"
authorId: "ag_65dmq8d1kw"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Passed up to the humans as ask ak_v8jvkwz7xr: Checks done: key is seen live, Resend refuses the send. The From domain in BLOG_MAIL_FROM does not match the verified root domain. Only Mitchell can change the Fly secret: filed as a do ask. Retest queued once he answers."
decidedBy: "ag_qtxi6eg1ul"
decidedAt: "2026-11-15T21:06:32.840Z"
sessionId: "se_bhdjfelbnw"
assignmentId: "as_2djo5kcme3"
costUsd: 0.45328860000000004
tokens: 22664
turns: 10
createdAt: "2026-11-15T21:05:27.830Z"
updatedAt: "2026-11-15T21:06:32.840Z"
---
## What I did
I ran the assigned checks against https://muster.town from my desk, using 2 of the 3 allowed POSTs. Then I looked up the public DNS records for the Resend sending domain through Cloudflare's DNS-over-HTTPS service. I updated the topic page [dc_6c572qf0b7](../../wiki/2026-11/2026-11-12-muster-town-blog-572qf0b7.md).

## Findings
- **Health:** commit `dc6a38003d2c`, startedAt `2026-11-15T20:51:43.137Z`. This is the restart from `fly secrets set`, about 1 min before Mitchell's 20:52 decision.
- **Honeypot probe:** `{"ok":true,"confirm":true}` HTTP 200. The server sees RESEND_API_KEY.
- **Real send to delivered@resend.dev:** `{"error":"We couldn't send the confirmation email. Try again in a minute.","code":"internal"}` HTTP 500. This means Resend refused the email (mailing-list.ts:155-157). The exact Resend message is only in the server log ("[mailing-list] confirmation email not sent") and in the Resend dashboard. I can't read either.
- **/blog:** HTTP 200. The form is `<form class="signup" ... data-source="index">`, and the page carries "Almost there: check your inbox and click the link to confirm."
- **DNS (what I saw):**
  - The Resend records are on the **root** domain: DKIM TXT at `resend._domainkey.muster.town`, and MX plus SPF at `send.muster.town`.
  - `mail.muster.town` has no records (NXDOMAIN).
- **Inference:** Mitchell verified `muster.town` in Resend. But BLOG_MAIL_FROM is probably `blog@mail.muster.town`, as our steps said, and Resend refuses a From address on a domain that isn't verified. The other possibility is that the domain is still pending verification in Resend. I can't tell these two apart from here.
- **Conclusion: Resend rejects.**

## What I need from you
Mitchell needs to do two things:
- Run `fly secrets set BLOG_MAIL_FROM="Muster Town <blog@muster.town>" -a muster-town`.
- Check that muster.town shows Verified in Resend. Its Emails log will also show the refused message and the reason.

Then queue one retest. It is a single POST to delivered@resend.dev, after a health startedAt later than his change.
