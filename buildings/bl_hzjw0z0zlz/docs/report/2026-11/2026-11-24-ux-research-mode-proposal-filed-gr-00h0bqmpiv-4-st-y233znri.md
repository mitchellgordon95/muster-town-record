---
id: "dc_lzy233znri"
type: "report"
state: "building"
title: "UX research mode proposal filed: gr_00h0bqmpiv, 4 steps, 750k, fund card in the queue"
authorId: "ag_ajexpcu9h0"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "gr_00h0bqmpiv filed with its fund card: Mitchell decides it in the decision queue, no further ask needed. Seam with UI/UX settled by tell to Teo (consent screen ours, capture + player his, shared admin-only research store from our step 1); recorded on topic page dc_0evlpy28i3."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-24T21:54:10.173Z"
sessionId: "se_z9s3hoohm7"
assignmentId: "as_07dt6sx12f"
costUsd: 0.7207582
tokens: 39408
turns: 7
createdAt: "2026-11-24T21:53:09.791Z"
updatedAt: "2026-11-24T21:54:10.173Z"
---
## What I did
Read Mitchell's 1:1 mt_8imtwy68zc (decision 1), checked the repo for recording and voice code and the media limits, and filed proposal gr_00h0bqmpiv with its fund card. Kelly's shape came in partway through and I followed it. Told Teo twice (en_ev189427_relay, en_ev189546_relay) and told Kelly (en_ev189551_relay). Wrote topic page [dc_0evlpy28i3](../../wiki/2026-11/2026-11-24-ux-research-mode-gr-00h0bqmpiv-vlpy28i3.md).

## Findings
- gr_00h0bqmpiv "UX research mode: friend link, recording, voice guide", filed against ob_508f35a2m4. The ask is 750,000 tokens. The estimate says 3 similar grants spent 515k–625k.
- Steps: (1) research link and consent screen (M): a one-use /research/<token> link that expires after 48 h, opens the town as a guest with no GitHub, and sends a Decline back to the plain homepage. (2) The guide as text chat in the sidebar (M). (3) Voice (L): the step opens with its own credential ask for a speech key stored as a collective secret. If the key is declined, the guide stays text chat only. (4) One real friend session and a report (S).
- Key results: kr_gzfypo2yfi, kr_92onyr88d7, kr_81o4ibyemd, kr_lygmb40bsh, kr_cwyx4ej95s.
- Where this differs from Kelly's shape: the recording and the replay page are not a step of our grant. They are UI/UX's work, and Teo files them as his own grant. kr_92onyr88d7 and step 4 depend on that grant.
- Design constraints: /api/media is public to anyone and capped at 8 MiB per file and 64 MiB per day (docs/multimedia.md; routes/media.ts:8). Recordings and transcripts therefore need a store only admins can read. The desk cannot capture audio, but the browser can. Main at e6b53093 has no recording, getUserMedia or realtime code.

## What I need from you
Mitchell needs to fund, counter or reject gr_00h0bqmpiv in the decision queue.
