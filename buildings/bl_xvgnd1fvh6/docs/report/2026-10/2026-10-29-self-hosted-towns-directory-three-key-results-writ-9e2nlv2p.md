---
id: "dc_dq9e2nlv2p"
type: "report"
state: "building"
title: "Self-hosted towns directory: three key results written under ob_kdym3851tm for Mitchell to keep or cut in the next rollup; jurisdiction question sent to Kelly (Onboarding), parked until Kelly answers"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_gadmvlnyjl","dc_7o0ucmpcaf","dc_bouobnr9ex","dc_v4iirqajou"],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Kelly has answered, so the parked continuation as_8yb9jl7sgs (read the answer, edit kr_8qeqmy2wt8 / kr_og03nxrkct / kr_esgajhpgiz to match) already resumed by itself; the rollup listing the three key results for Mitchell follows once that edit lands, so he sees them once in final wording."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T04:28:08.263Z"
sessionId: "se_r8jyjtlyqr"
assignmentId: "as_hu7qobiguu"
costUsd: 1.54688695
tokens: 30938
turns: 19
createdAt: "2026-10-29T04:27:17.975Z"
updatedAt: "2026-10-29T04:28:08.263Z"
---
## What I did
From the 1:1 with Mitchell (mt_mqq87d7zoo, notes [dc_gadmvlnyjl](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md), note [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md)): read Kelly's Onboarding page [dc_bouobnr9ex](../../../../bl_hzjw0z0zlz/docs/wiki/2026-10/2026-10-29-hosted-collectives-live-state-and-checks-uobnr9ex.md) and docs/hosted-collectives.md to see what Onboarding owns, sent Kelly (ag_s1n1xknj8n) a concrete jurisdiction question by tell (ms_9i14iz0uw6; Kelly was idle, so the town queued it as Kelly's assignment as_kk3vf82amk), then wrote three key results under objective ob_kdym3851tm with my default assumption stated. Wrote a Prod topic page "Self-hosted towns directory" ([dc_v4iirqajou](../../wiki/2026-10/2026-10-29-self-hosted-towns-directory-iirqajou.md)) and the matching wiki page. No code, no proposal.

## Findings
- **Ownership today.** Onboarding owns the homepage tiles (the hub list of hosted collectives) and the root GitHub sign-in (hosted collectives grant gr_rdyrjzclfe). Prod owns deployment, health, backup and monitoring. Nothing in the repo covers self-hosting at your own domain: README.md covers running from source, deploy/ is Fly-specific; no directory table, route or page exists.
- **Two questions to Kelly.** (1) Listing: self-hosted towns as tiles on the homepage Onboarding owns (Onboarding UI, Prod API) or a separate Prod page at muster.town/directory with the homepage untouched. (2) Sign-up: registration behind the root GitHub sign-in (one town per GitHub id, like Start a collective) or DNS proof only, no account.
- **Default until Kelly answers:** Prod owns the self-host docs, the register/verify API and a /directory page; DNS proof only; homepage untouched (touching it is Onboarding's code and needs Mitchell's go-ahead under the merge rules dc_xsrxxbfa7i).
- **Key results on the Prod board (all not-started, no grant yet; the next rollup lists them so Mitchell can keep or cut):**
  - kr_8qeqmy2wt8 Self-host path: one docs page (docs/self-host.md: Docker image or compose, env, GitHub OAuth app, backups) takes a stranger to a running town at their own domain; checked by bringing one up from those docs on a throwaway box at a test domain.
  - kr_og03nxrkct Registration and verification, no approval (Mitchell's rule): POST /api/directory/register returns a token, proof by DNS TXT record or well-known URL, verified + lastSeenAt, stale never deleted; checked by one real registration end to end.
  - kr_esgajhpgiz Listing: a public page on muster.town lists verified self-hosted towns alongside our collectives (name, URL, goal, verified, last seen); GET /api/directory returns the same JSON.
- Parked on Kelly's assignment as_kk3vf82amk: when it ends I read the reply and edit the key results' wording and ownership to match, then they go into the next Prod rollup (due on the test-alert result or 24 h after #15).

## What I need from you
Nothing needed (Mitchell keeps or cuts the three key results from the next Prod rollup).
