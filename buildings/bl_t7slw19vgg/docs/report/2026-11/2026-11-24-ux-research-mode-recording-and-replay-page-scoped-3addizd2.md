---
id: "dc_m43addizd2"
type: "report"
state: "building"
title: "UX research mode recording and replay page scoped; proposal gr_oi1nj61b6t filed (350k, 3 steps)"
authorId: "ag_8ckpaf7bdm"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Proposal gr_oi1nj61b6t and its ask card are in the decision queue; the fund decision is Mitchell's and comes back on the grant's thread. Seam told to Kelly (ms_106emi80cr). Nothing more to queue until he decides."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-24T22:11:10.447Z"
sessionId: "se_9fbix5givk"
assignmentId: "as_hkw3ids34a"
costUsd: 0.9765576
tokens: 48828
turns: 17
createdAt: "2026-11-24T22:10:22.121Z"
updatedAt: "2026-11-24T22:11:10.447Z"
---
## What I did
Read Onboarding's gr_00h0bqmpiv thread and the media, permission, backup, data-dir and renderer code on main 356445fb. Wrote the design [dc_yh5nowmqhp](../../note/2026-11/2026-11-24-ux-research-mode-session-recording-and-the-replay-5nowmqhp.md). Filed proposal gr_oi1nj61b6t "Record research sessions and replay them" with its ask card. Told Kelly the seam (ms_106emi80cr). Started topic page [dc_0404v7yqff](../../wiki/2026-11/2026-11-24-ux-research-mode-recording-and-replay-gr-oi1nj61b6-04v7yqff.md).

## Findings
- **/api/media cannot hold recordings.** It is public to read (server routes/media.ts:6-9, :23). It is capped at 8 MiB per file and 64 MiB per uploader per day (core media.ts:13-14, checked at :46 and :56). Its files are BLOBs in town.db (media.ts:3), so they would bloat the hourly backup. Kelly's numbers are confirmed.
- **Admin check:** `permissions.requireAdmin` (core permissions.ts:94), as used in routes/town.ts:122.
- **Recording:** rrweb records the DOM, with the map canvas blocked. The map is a 2D canvas (renderer.ts:165), so toBlob works. We add our own WebP snapshot of it every 2 s (≤640 px, unchanged frames skipped), plus an action trail (routes, panels, places, buttons, chat lines) as rrweb custom events in the same stream.
- **Size:** an estimated 10–25 MB per 20-minute session. This is not measured; step 1 measures it. The hard cap is 60 MB, and map snapshots drop to one every 10 s past 40 MB.
- **Time base:** the server's `startedAt` from the start call. Events are placed at `timestamp − clientStartMs`. Transcript lines are placed at `serverTs − startedAt`. Skew is at most half the start call's round trip, and that round trip is stored with the recording.
- **Store:** ndjson.gz chunks under `<dataDir>/research/<rsId>/`. The browser posts one every 10 s or at 512 KB, and by sendBeacon on pagehide. Seq numbers make retries idempotent.
  - Only the consented friend's user can write. Reads are admin-only, with no-store headers.
  - Recordings are deleted after 30 days and are left out of the off-site backup. That backup holds town.db and transcripts only (backup/index.ts:41-50). The volume is 10 GB (deploy/README.md:8).
- **Page:** `#/research` lists sessions. `#/research/<id>` shows the replay on the left with map snapshots painted over the canvas box and the transcript on the right. One timeline with markers runs under both, and clicking a line seeks the replay there.
- **Proposal gr_oi1nj61b6t, 350k:**
  1. Recorder and private store (M)
  2. Research page (M)
  3. Live check, retention and docs (S)
- **Key results:** kr_9yx3rdnmen, kr_tzavcdfseq, kr_f17zyhemtq. The estimate line puts 3 similar grants at 246k–353k spent.
- **Seam asked of Onboarding's step 1:**
  - `/api/me.researchSession {id, status: invited|consented|declined|ended, consentedAt}`
  - a server read giving the friend's userId and status
  - transcript lines `{at: server ISO, speaker, text}` per session
- **Risk:** rrweb 2.x is still alpha, and 1.1.3 is the last stable release. Step 1 pins one.
- Kelly is idle, so the tell waits for their next session.

## What I need from you
Fund, counter or reject gr_oi1nj61b6t in the decision queue.
