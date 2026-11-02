---
id: "dc_9oka3bqhxb"
type: "report"
state: "building"
title: "Hosted collectives step 2 live check: 8ecf110 is live, the anonymous and return_to checks pass, no `demo` exists yet; GitHub sign-in check filed for Mitchell (dc_3oslgrfo6j)"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 2 live-verified: 8ecf110 ⊆ 086eeff live, anonymous and return_to checks pass, bad return_to dropped from the state cookie. Demo checks wait on Mitchell (dc_chdfylcjva, dc_3oslgrfo6j); they'll be a short follow-up once he answers."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T21:16:51.200Z"
sessionId: "se_squ9y4va1a"
assignmentId: "as_y0chyp5cb7"
costUsd: 0.5109019
tokens: 25545
turns: 17
createdAt: "2026-10-27T20:46:31.745Z"
updatedAt: "2026-10-27T21:16:51.200Z"
---
## What I did
I ran checks 1–5 against muster.town with curl and headless Chromium (hubcheck.mjs), at 2026-10-27 20:45Z. I didn't change any code. I filed the human sign-in check in the outbox.

## Findings
1. **Commit and fixture.** **Pass on the commit.** /api/health reports commit 086eeff, and `git merge-base --is-ancestor 8ecf110 086eeff` succeeds. `hosted.count` is **0**, so `demo` doesn't exist yet ([dc_chdfylcjva](../../../../../town-hall/outbox/2026-10/2026-10-27-create-the-demo-hosted-collective-on-muster-town-a-dfylcjva.md) is still open).
2. **Anonymous visitor. Pass.**
   - /workshop/ returns 200. The guest card shows "Sign in with GitHub" behind the "Watch, then join" overlay, with 0 console errors. Screenshot: /home/agent/shots/hub2/1.png on my desk.
   - /api/me returns 401. /nope/ returns 302 to `/`.
   - `/auth/github?return_to=https://evil.test/demo/` and `?return_to=/nope/` both return 302 to github.com/login/oauth/authorize. Both have `redirect_uri=https://muster.town/auth/github/callback` and set the signed `at_oauth_state` cookie (Path=/auth, HttpOnly, Secure, 600 s).
   - The decoded cookie payload for both is `{state, iat}` with **no returnTo**, so the bad value is dropped. The callback would then fall back to the default, /workshop/. For comparison, `?return_to=/workshop/` keeps `"returnTo":"/workshop/"` in the payload. Nothing points off-site.
3. **Agent token. Unchanged.** Root /api/me with my agent token returns 403 `"This endpoint needs a user token, not an agent token."` (requireUser, context.ts:86). That was already the response before this change: it's the endpoint's normal answer to an agent token, and 8ecf110 doesn't touch it. /demo/api/me returns 302 to `/`, because no hosted collective exists, so I couldn't test the 401 for a pasted token in a hosted World (Tae's finding 2).
4. **Demo checks. Skipped:** `demo` doesn't exist. /demo/, /demo/auth/github and /demo/api/me all return 302 to `/`. The step 1 fixture checks (400 for a "workshop" slug, 409 for a duplicate) still need a token from a human admin.
5. **GitHub sign-in.** Filed outbox request **[dc_3oslgrfo6j](../../../../../town-hall/outbox/2026-10/2026-10-27-sign-in-once-on-muster-town-and-confirm-your-role-slgrfo6j.md)** (observation). It asks Mitchell to sign in once, create `demo` if needed, open /demo/ without a second GitHub prompt, then check that /demo/api/me says admin and /api/me shows his Workshop role. Asking to join with a second account is optional.

## What I need from you
Nothing needed. Once Mitchell creates `demo` ([dc_chdfylcjva](../../../../../town-hall/outbox/2026-10/2026-10-27-create-the-demo-hosted-collective-on-muster-town-a-dfylcjva.md)) and answers [dc_3oslgrfo6j](../../../../../town-hall/outbox/2026-10/2026-10-27-sign-in-once-on-muster-town-and-confirm-your-role-slgrfo6j.md), the demo checks (4, and the hosted 401 in 3) are one short session.
