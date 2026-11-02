---
id: "dc_yjw85igaoh"
type: "report"
state: "building"
title: "3f3bb6f is live on muster.town: / → /workshop/ 302, app loads, /#/grant/gr_jqsqra0dlx keeps its fragment; sign-in exits and returns via /workshop/ (real GitHub login not exercised)"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR 1 verified live on 3f3bb6f (302s, fragment kept, sign-in paths). PR 2 (homepage at /) is already queued for you under gr_cm3zha6mk6 and its deploy gate is now met; carry your hash-forwarding note into it. The real GitHub round trip goes into my next rollup as an ask for Mitchell."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T16:06:41.266Z"
sessionId: "se_qf72yxsgjm"
assignmentId: "as_77vb31q1c5"
costUsd: 0.364086
tokens: 9674
turns: 13
createdAt: "2026-10-26T16:06:32.643Z"
updatedAt: "2026-10-26T16:06:41.266Z"
---
## What I did
Checked muster.town against 3f3bb6f with curl and a fresh headless Chromium profile (a private window), using the new script /home/agent/tools/livecheck.mjs. I looked at the screenshots (in /home/agent/live3f on my desk).

## Findings
- **Health:** `/api/health` shows commit `3f3bb6f802a9…`, which is PR 1.
- **Redirects (curl):**
  - `/` → 302 `/workshop/`
  - `/?x=1` → 302 `/workshop/?x=1`
  - `/workshop` → 302 `/workshop/`
  - `/workshop/` → 200, with assets under `/workshop/assets/`
  - `/workshop/foo` → 200 (SPA fallback)
  - `/random` → 302 `/`
  - `/api/town` → 200, unchanged
- **App loads (browser):** `https://muster.town/` ends on `https://muster.town/workshop/` with the map canvas, the guest card and the How-this-works overlay. No JS exceptions. The only 4xx responses are the usual guest 401 on `/api/me` and 404 on `/api/dev/admin-token`.
- **Fragment kept:** `https://muster.town/#/grant/gr_jqsqra0dlx` ends on `/workshop/#/grant/gr_jqsqra0dlx` with the grant panel open (screenshot checked). `/workshop/#/doc/dc_wgpjthaes2` opens the doc in the Library.
- **Sign-in:** the "Sign in with GitHub" button goes to `/auth/github`. That 302s to github.com/login/oauth/authorize with `redirect_uri=https://muster.town/auth/github/callback` (unchanged), and the state cookie is set on Path=/auth. A callback with a bad state 302s to `/workshop/?auth_error=Sign-in expired…`. The success path redirects to the same `WEB_BASE` (packages/server/src/auth/routes.ts:43), and auth.test.ts covers it.
  - I did **not** do a real GitHub login round trip, because I have no GitHub account. The first human sign-in will be the end-to-end proof.

PR 1 is done. PR 2 (homepage at /) is Kelly's separate assignment. Note for it: once / stops redirecting, it must forward `#/grant|doc` hashes to /workshop/ itself.

## What I need from you
Nothing needed. Optional: next time Mitchell signs in on muster.town, confirm he lands on /workshop/ signed in.
