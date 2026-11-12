---
id: "dc_ptxk3t2xre"
type: "report"
state: "building"
title: "Blog email signup PR #433 opened (form at the foot of each post, subscribe API, admin CSV export); parked on its CI to merge"
authorId: "ag_wcn8hkzy0s"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #433 opened as draft; the merge continuation as_ieeocm91dj is parked on its CI and will verify migration 112 is still unique before merging. Nothing live yet; it goes into rollup #4 once the signup form is verified live."
decidedBy: "ag_qtxi6eg1ul"
decidedAt: "2026-11-12T16:07:39.409Z"
sessionId: "se_7sqpw395sr"
assignmentId: "as_k1oe6hzp3d"
costUsd: 1.0247183000000002
tokens: 51236
turns: 25
createdAt: "2026-11-12T16:07:30.717Z"
updatedAt: "2026-11-12T16:07:39.409Z"
---
## What I did
I built Mitchell's email signup for the blog (mt_msnjkpgwdb decision 7) and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/433. Before merging I told Cleo (ms_kvw0l8a1e6). I'm parked on the PR's CI.

## Findings
- **Form:** every post page has a one-field signup form in its footer, after the article. The /blog index has one too. Its copy is "New posts by email. Nothing else.". A small inline script posts JSON and replaces the form with "Thanks, you're on the list."; errors show inline. The form needs no bundle. The code is `signup()` in `packages/server/src/blog.ts`.
- **API:** the new file `packages/server/src/mailing-list.ts` is registered on the root app next to blogRoutes.
  - `POST /api/blog/subscribe {email, source}` is public and needs no sign-in.
  - It trims and lowercases the address. It accepts only one @, a dot in the domain, no spaces and at most 254 characters; anything else gets a 400 `bad_request`.
  - A repeat signup inserts nothing and still answers `{ok:true}`.
  - A hidden honeypot field `website` drops bots silently.
  - Each client IP may post 10 times an hour, then gets 429 `rate_limited`. The IP comes from `fly-client-ip` on Fly, else the socket address.
  - `GET /api/blog/subscribers` is admin-only (requireUser plus requireAdmin). It returns `{count, subscribers:[{email, createdAt, source}]}`, or a CSV download with `?format=csv`.
- **Storage:** migration `112_mailing_list.sql` adds one table (email primary key, createdAt, source, unsubscribedAt). On origin/main the highest migration was 111 just before the push. The table is in the town's SQLite database, so Prod's backups include it.
- **No confirmation email:** the town has no mail sender, and Mitchell asked for "just a simple input". There is no unsubscribe link yet.
- **Docs and log:** docs/blog.md has a new "The email signup" section with the curl commands for the export. The log line is docs/log.d/2026-11-12-juno-1-email-signup.md.
- **Verified locally:** 11 tests pass in mailing-list.test.ts and blog.test.ts. They cover subscribe, lowercasing, deduping, a bad address (400), the honeypot, the 429 rate limit, refusing non-admins and guests (403 and 401), CSV export, and the form's placement. `npm run typecheck` is clean. Nothing is live yet.

## What I need from you
Nothing needed.
