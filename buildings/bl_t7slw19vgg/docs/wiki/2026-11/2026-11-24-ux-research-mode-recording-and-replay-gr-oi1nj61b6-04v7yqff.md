---
id: "dc_0404v7yqff"
type: "wiki"
state: "building"
title: "UX research mode: recording and replay (gr_oi1nj61b6t)"
authorId: "ag_8ckpaf7bdm"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-24T22:10:10.203Z"
updatedAt: "2026-11-24T22:10:10.203Z"
---
Directed by Mitchell in 1:1 mt_8imtwy68zc (2026-11-24). Onboarding's gr_00h0bqmpiv builds the friend link and consent screen, the text guide, the voice guide and the first friend session. Its key result kr_92onyr88d7 and its step 4 wait on our part.

**Ours:** proposal gr_oi1nj61b6t "Record research sessions and replay them". 350k, 3 steps M/M/S, filed 2026-11-24, not funded yet. Design and citations: [dc_yh5nowmqhp](../../note/2026-11/2026-11-24-ux-research-mode-session-recording-and-the-replay-5nowmqhp.md). Its key results:
- kr_9yx3rdnmen: private store, non-admin gets 403
- kr_tzavcdfseq: Mitchell replays a session beside its transcript
- kr_f17zyhemtq: nothing recorded without consent, and under 60 MB per 20 minutes

**Design in short:**
- rrweb records the DOM. The map canvas is blocked from rrweb. Instead, a WebP snapshot of the map every 2 s (≤640 px) and an action trail go in as custom events.
- Chunks are ndjson.gz files under `<dataDir>/research/<rsId>/`, never /api/media (public, 8 MiB per file and 64 MiB a day: core media.ts:13-14). Admin reads go through requireAdmin (permissions.ts:94). Recordings are deleted after 30 days and are not in the off-site backup.
- Time base: the server's `startedAt` from the start call. Every event and transcript line is placed in ms from it.

**Seam asked of Kelly (told 2026-11-24):**
- /api/me.researchSession `{id, status, consentedAt}`
- a server read with the friend's userId
- transcript lines `{at, speaker, text}` per session

Size per session (10–25 MB) is an estimate. Step 1 measures it.
