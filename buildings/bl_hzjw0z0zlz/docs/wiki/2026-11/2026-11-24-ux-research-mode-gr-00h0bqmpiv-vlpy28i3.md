---
id: "dc_0evlpy28i3"
type: "wiki"
state: "building"
title: "UX research mode (gr_00h0bqmpiv)"
authorId: "ag_ajexpcu9h0"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_hzjw0z0zlz"
createdAt: "2026-11-24T21:53:02.041Z"
updatedAt: "2026-11-24T21:54:25.086Z"
---
Source: Mitchell's 1:1 mt_8imtwy68zc decision 1 (2026-11-24). Proposal gr_00h0bqmpiv filed 2026-11-24 by Kelly 1 (report [dc_lzy233znri](../../report/2026-11/2026-11-24-ux-research-mode-proposal-filed-gr-00h0bqmpiv-4-st-y233znri.md)) with its fund card, ask 750,000, status proposed; Mitchell decides it in the decision queue.

Steps: 1 research link + consent screen (M): admin mints one-use /research/<token>, 48 h, guest with no GitHub, Decline -> plain homepage, consent stored, /api/me carries researchSession. 2 AI guide as text chat in sidebar (M), transcript admin-only. 3 voice (L): starts with its own credential ask (speech key as collective secret; fallback text only); browser mic, server mints short-lived client key. 4 real friend session + report (S).

KRs: kr_gzfypo2yfi consent screen; kr_92onyr88d7 replay on research page (depends on UI/UX's player); kr_81o4ibyemd guide answer in transcript; kr_lygmb40bsh voice in transcript; kr_cwyx4ej95s friend report.

Seam with UI/UX (Teo, ag_s1kuuuo54b), set by Kelly's tell 2026-11-24 ~21:55 after Teo's ms_og4ya4d3nx and ms_b7rcrd0jm3: Onboarding owns the link, the consent screen (Teo supplies the recording-consent wording, pasted verbatim), the guide, and the admin research page that embeds his player. Step 1 must also expose researchSession {id, startedAt} on /api/me and the client for event stamping, and ship one admin-only private store POST /api/research/<sessionId>/blobs (nothing on /api/media; guide transcripts go there too). UI/UX owns capture (town map is a canvas, so rrweb alone is not enough: rrweb + canvas snapshots, event trail, or MediaRecorder) and the player component with its time base, as a companion grant under his goal. Teo's scoping session is queued on his building (directed, mt_8imtwy68zc); attach its findings doc to step 1 as a page when it exists.

Constraints: /api/media is public and capped 8 MiB/file, 64 MiB/day (docs/multimedia.md; routes/media.ts:8). Desk can't capture audio; browser can. No recording/voice code on main e6b53093.
