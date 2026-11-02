---
id: "dc_bavdbf1sr5"
type: "report"
state: "building"
title: "Self-hosted towns directory: Kelly's answer read, the three key results under ob_kdym3851tm rewritten to final wording with ownership (homepage tiles by Onboarding on Prod's GET /api/directory, DNS proof only); ready for rollup #16"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_gadmvlnyjl","dc_7o0ucmpcaf","dc_dq9e2nlv2p","dc_v4iirqajou"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Final wording of the three directory key results is on the board; rollup #16 lists them for Mitchell. Grants proposed after his keep/cut, kr_og03nxrkct first."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T04:31:08.879Z"
sessionId: "se_s02om3gfxj"
assignmentId: "as_8yb9jl7sgs"
costUsd: 1.4258421499999998
tokens: 28517
turns: 14
createdAt: "2026-10-29T04:30:41.817Z"
updatedAt: "2026-10-29T04:31:08.879Z"
---
## What I did
Read Kelly's answer (tell ms_yegpj7v9cq, 2026-10-29 04:27Z, answering for Mitchell from 1:1 mt_mqq87d7zoo), checked the repo facts Kelly cited against main (f91838c), and edited kr_8qeqmy2wt8, kr_og03nxrkct and kr_esgajhpgiz with `set_key_result` (all still under ob_kdym3851tm, sources [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md) and [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md), all not-started, no grant). Rewrote the Prod topic page "Self-hosted towns directory" ([dc_v4iirqajou](../../wiki/2026-10/2026-10-29-self-hosted-towns-directory-iirqajou.md)) and my wiki page with the settled jurisdiction. No code, no PR: this assignment was wording and ownership only.

## Findings
- **Kelly's answers.** (1) Listing: verified self-hosted towns appear as tiles on the muster.town homepage next to the Workshop; Onboarding adds a third tile source in home.ts collectives() reading Prod's `GET /api/directory` (shape `{towns:[{host,url,name,goal,verifiedAt,lastSeenAt}]}`). A separate /directory page is optional, not needed. (2) Sign-up: DNS proof only, no GitHub account (a login proves nothing about domain control); one entry per host, rate-limited verify; removal = drop the proof, the re-check delists. Name and goal come from the registered town's own `GET /api/collectives`, liveness from its `/api/health`; list only if seen within 24 h, delist after a few days unseen.
- **Verified against main:** home.ts builds tiles from own town + hub list + placeholder (line 21); the footer link "Run Muster Town on your own server" points at the README (line 111); `GET /api/collectives` exists (app.ts line 191); no docs/self-host.md and no directory code exist yet.
- **Final key results (on the Prod board):**
  - kr_8qeqmy2wt8 Self-host path (Prod): one docs page (docs/self-host.md: Docker image or compose, env, GitHub OAuth app, backups, directory registration) takes a stranger to a running town at their own domain; proven on a throwaway box at a test domain, never muster.town; the homepage footer link points at the page.
  - kr_og03nxrkct Registration, no approval and no account (Prod): `POST /api/directory/register` returns a token; proof by TXT record `_muster-town.<host>` or `GET https://<host>/.well-known/muster-town`; one entry per host; dropping the proof delists; checked by one real registration end to end.
  - kr_esgajhpgiz Listing: `GET /api/directory` (Prod) returns verified towns seen within 24 h, and each shows as a "self-hosted" tile on the homepage next to the Workshop (Onboarding), opening at its own domain.
- **Ownership split:** Prod = docs page, register/verify API, `GET /api/directory`, last-seen re-check. Onboarding = homepage tiles, repointing the footer link, manual mention; Kelly assigns the tile work once the API shape is on main (I tell Kelly then).
- **Next (manager work, not this assignment):** rollup #16 lists the three key results for Mitchell to keep or cut; after that, propose grants, kr_og03nxrkct (API + docs) first since the listing depends on it.

## What I need from you
Nothing needed (Mitchell keeps or cuts the three key results from Prod rollup #16).
