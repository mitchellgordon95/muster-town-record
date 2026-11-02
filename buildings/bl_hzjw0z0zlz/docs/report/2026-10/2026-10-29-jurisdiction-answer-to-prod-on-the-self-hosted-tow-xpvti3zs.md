---
id: "dc_yhxpvti3zs"
type: "report"
state: "building"
title: "Jurisdiction answer to Prod on the self-hosted towns directory: homepage tiles (Onboarding UI on Prod's GET /api/directory), DNS proof only, no GitHub account (ms_yegpj7v9cq)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_gadmvlnyjl","dc_xsq7zncdvj","ms_yegpj7v9cq"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged: Prod answered by tell ms_yegpj7v9cq, ownership split recorded on topic page dc_xsq7zncdvj. Tile work waits on Cleo's \"/api/directory shape is on main\" and then goes to the building queue as exploration under kr_z0mj5teeu7."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-29T04:29:21.362Z"
sessionId: "se_dtj6mn0hol"
assignmentId: "as_kk3vf82amk"
costUsd: 1.53791875
tokens: 30758
turns: 17
createdAt: "2026-10-29T04:29:01.838Z"
updatedAt: "2026-10-29T04:29:21.362Z"
---
## What I did
Read Cleo's 1:1 notes with Mitchell ([dc_gadmvlnyjl](../../../../bl_xvgnd1fvh6/docs/meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-cleo-notes-dmvlnyjl.md)) and the homepage code (packages/server/src/home.ts `collectives()`), then answered Cleo (ag_imxsagd9cj) by tell ms_yegpj7v9cq. Recorded the ownership split on the topic page "The stranger's first minute" ([dc_xsq7zncdvj](../../wiki/2026-10/2026-10-29-the-stranger-s-first-minute-homepage-workshop-kr-1-q7zncdvj.md), new section) and in my Notes. No code changed.

## Findings
- **Listing page: homepage tiles, not a separate page.** Mitchell's objective ob_kdym3851tm says self-hosted towns are "listed alongside muster.town", and the homepage is the only list a stranger sees (KR kr_z0mj5teeu7). The homepage already composes its tiles from the own town, the hub list and a placeholder, so a third source is a small Onboarding change (home.ts + HomeCard.tsx Tile: host shown, "self-hosted" marker, no live preview cross-origin). Prod serves GET /api/directory; a Prod /directory table page is optional, not needed for the KR.
- **API shape asked of Prod:** `{towns:[{host,url,name,goal,verifiedAt,lastSeenAt}]}`. Name and goal come from the registered town's own GET /api/collectives (every Muster Town server serves it), liveness from its GET /api/health; list only towns verified and seen within 24 h, delist after days unseen, one entry per host.
- **Sign-up: DNS proof alone, no GitHub account.** A GitHub login proves nothing about domain control; Mitchell said no approval. The one-per-GitHub-id cap on Start a collective exists because hosted collectives spend our server; a directory row costs nothing, so cap per host and rate-limit verify instead. Removal = drop the TXT record or well-known file. Suggested the well-known route be served by the self-hosted server itself from an env var, the least confusing path for someone who has never touched DNS.
- **Ownership:** Prod = self-host docs, register/verify, /api/directory, re-check, optional /directory. Onboarding = homepage tiles, repointing the footer "Run Muster Town on your own server" link at Prod's self-host page, the manual mention; the staleness sweep (KR 6) then keeps them current.
- **Next on our side:** assign the tile work as exploration under kr_z0mj5teeu7 (pages [dc_xsq7zncdvj](../../wiki/2026-10/2026-10-29-the-stranger-s-first-minute-homepage-workshop-kr-1-q7zncdvj.md) + style guide) once Cleo confirms the /api/directory shape is on main. Nothing to assign yet. Mitchell keeps or cuts Cleo's key results in Prod's next rollup, so this needs no Onboarding rollup.

## What I need from you
Nothing needed.
