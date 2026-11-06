---
id: "dc_d66ylg0kmq"
type: "report"
state: "building"
title: "Publish to GitHub live check: code live and tested, but no repo set yet, so nothing has pushed; grant not ready to close"
authorId: "ag_m3yu10owu8"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Agreed: KR1/KR2 built, tested and live but unexercised; the only missing piece is Mitchell's empty repo URL, which already has its channel (outbox dc_wawcjkger2, claimed by him). Not closing gr_30f8obzab8 yet. A one-shot re-check goes on the schedule for later today."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-06T04:26:38.460Z"
sessionId: "se_3blt9g1je9"
assignmentId: "as_h1c2w1iyzp"
costUsd: 0.5666209999999999
tokens: 28331
turns: 14
createdAt: "2026-11-06T04:26:25.122Z"
updatedAt: "2026-11-06T04:26:38.460Z"
---
## What I did
I read the live /api/health and /api/town for the root Workshop and both hosted collectives (trauma, hollyville) at 04:25Z, with 5dc50c7 live. I traced how a hosted World's export finds its publish target and ran the publish tests in core and server. I rewrote the topic page [dc_0ub741sboo](../../wiki/2026-11/2026-11-04-publish-to-github-gr-30f8obzab8-b741sboo.md). I made no code changes because there was no push error to fix.

## Findings
- **No repo is set yet.** GET /api/town returns no `town.publish` key on the Workshop, /trauma/ or /hollyville/. In /api/health `export`, every collective shows `lastAt` 03:26Z, `lastPushAt: null` and `pushError: null`. So nothing has been pushed, and nothing has failed either. Outbox dc_wawcjkger2 has been claimed by Mitchell since 11-05 19:48Z and isn't done. There is no repo to open.
- **KR1 kr_gyqktjpevz (Settings block):** it has been live since 7fb234a and 2e8704f. The routes are admin-only (server routes/town.ts:336-347). The token never comes back from the API, which server publish.test.ts:12 checks. Tests are green. Nobody has saved a repo live yet.
- **KR2 kr_bm7q7rwxrk (hourly push, failure shown):** the hourly export runs live (lastAt 03:26Z, commit 56c182f). The push code is core export.ts:279-280 and the outcome is recorded by world.ts:565. core publish.test.ts covers a push landing, a failure with the token masked, and catching up after a failure; 8 of 8 pass. It can't be checked live until a repo is set.
- **KR3 kr_sqbsdpaju8 (each hosted collective pushes only to its own repo):**
  - **What the code guarantees:** each hosted collective gets its own World and app (main.ts:116-121) and its own runtime with its own exportDir (main.ts:106). That runtime calls `world.exportOffThread` (runtime index.ts:691), which reads `publishTarget()` from that World's own town settings and secrets (world.ts:536-551). So one collective's export can't reach another's repo, and the GH_TOKEN fallback is also the collective's own.
  - **Test:** core publish.test.ts:135 "hosted isolation" is green.
  - **Live:** trauma and hollyville each export hourly with their own commits (1d05564 and edf5b5f). PUT /<slug>/api/town/publish answers 401 without sign-in on both, so the route is there for each hosted app.
  - **Unverified:** a hosted owner saving a repo and its push landing. That needs a hosted admin's sign-in, which the second GitHub test account could get by starting its own collective.
- **Recommendation:** don't close the grant yet. KR1 and KR2 are on-track: built, tested and live, but never exercised. Only Mitchell's empty repo URL is missing, and the next hourly export would then prove both. After that, the test account can verify KR3 live (due 11-10).

## What I need from you
Mitchell: create an empty GitHub repo (no README) and paste its URL in Town Hall → Settings → Publish to GitHub (the token is optional; without one it uses GH_TOKEN), then Save.
