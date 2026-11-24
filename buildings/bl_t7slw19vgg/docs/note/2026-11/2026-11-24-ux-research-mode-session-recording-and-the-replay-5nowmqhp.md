---
id: "dc_yh5nowmqhp"
type: "note"
state: "building"
title: "UX research mode: session recording and the replay page (design, UI/UX part)"
authorId: "ag_8ckpaf7bdm"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["mt_8imtwy68zc","gr_00h0bqmpiv"],"urls":["https://github.com/rrweb-io/rrweb"]}
tags: ["research-mode","recording","design"]
createdAt: "2026-11-24T22:09:18.093Z"
updatedAt: "2026-11-24T22:09:18.093Z"
---
Directed by Mitchell in 1:1 mt_8imtwy68zc (2026-11-24). Onboarding's grant gr_00h0bqmpiv builds the friend link and consent screen (its step 1), the text guide (2), the voice guide (3) and the first friend session (4). Its key result kr_92onyr88d7 ("a recording replays on the research page, admins only") and step 4 wait on this part. UI/UX owns (a) the recording and its private store and (b) the research page.

## What the code says (main at 356445fb)
- `/api/media` is public and capped: `MEDIA_MAX_BYTES = 8 MiB` and `MEDIA_DAILY_BYTES = 64 MiB` per uploader per day (packages/core/src/media.ts:13-14, checked at :46 and :56); GET serves anyone, "the town is public to read" (packages/server/src/routes/media.ts:6-9, :23). Media are BLOBs in town.db (media.ts:3), so they also bloat the hourly backup. Not usable for recordings.
- Admin check: `world.permissions.requireAdmin(holder, msg)` throws the one 403 (packages/core/src/permissions.ts:94); used e.g. at packages/server/src/routes/town.ts:122 and packages/server/src/mailing-list.ts:175.
- The map is a 2D canvas (packages/web/src/map/renderer.ts:165 `getContext("2d")`), so `canvas.toBlob` works without preserveDrawingBuffer. A DOM recorder alone shows a blank map.
- Data dir: `<dir>/data` holds town.db (packages/server/src/hub.ts:266-268); live it is /data/workshop/data on a 10 GB Fly volume (deploy/README.md:8-10). The off-site backup copies town.db and the transcripts dir only (packages/server/src/backup/index.ts:41-50).
- Nothing in the repo uses rrweb yet, and nothing names `researchSession` yet.

## Decision 1: how to record: both, in one stream
- **DOM:** rrweb `record()` (MIT) for the React panels, sheets, HUD and chat. `maskAllInputs` off except password and token fields (`maskInputOptions: {password: true}` plus a `.rr-mask` class on secret fields); `blockClass` on the map canvas so rrweb does not try to serialise it.
- **Map:** our own snapshot of the map canvas every 2 s, downscaled to at most 640 px wide, WebP quality 0.6, skipped when the frame is unchanged (cheap hash of a 32×18 thumbnail). Each snapshot goes into the same stream as an rrweb custom event `{tag: "map", data: {w, h, webp}}`. Replay paints it over the canvas's box.
- **Action trail:** custom events in the same stream for what the replay alone makes hard to search: route/hash changes, panel opened and closed (kind, id), place walked to, button labels pressed, chat lines sent. These make the timeline markers on the research page.
- Not chosen: rrweb's built-in `recordCanvas` with sampling records full-resolution frames (larger), and a server-side-only trail cannot show what the friend saw.

**Size per 20-minute session (an estimate, not measured; step 1 measures it on the mock):** DOM full snapshot about 0.2–0.5 MB plus incremental 1–5 KB/s, so 1.5–6.5 MB raw, about 0.3–1.5 MB gzipped. Map: up to 600 snapshots × 15–35 KB = 9–21 MB (fewer when the map is idle). Total about 10–25 MB per session. Hard cap 60 MB per session; the recorder drops map snapshots to one every 10 s past 40 MB.

**Time base.** `POST /api/research/<rsId>/recording` returns the server's `startedAt` (ISO, server clock). The client keeps `clientStartMs = Date.now()` at that response and sends it in each chunk's header. Every event's position is `t = event.timestamp − clientStartMs` (ms from the start). A transcript line Onboarding stores with a server timestamp sits at `t = serverTs − startedAt`. Clock skew between the two is at most half the start call's round trip; the server records that round trip with the recording.

## Decision 2: private store
- Files, not town.db: `<dataDir>/research/<rsId>/meta.json` and `<seq>.ndjson.gz` chunks. The browser posts a chunk every 10 s or at 512 KB, whichever first, and on `pagehide` by `sendBeacon`; each POST at most 1 MiB, seq numbers make retries idempotent.
- Write: `POST /api/research/<rsId>/chunks` is taken only from the signed-in user that `/api/me.researchSession` names, while that session is consented and open (Onboarding's step 1 owns that state). Anyone else gets 403.
- Read: `GET /api/research` (list) and `GET /api/research/<rsId>/events?from=<seq>` and `/transcript` pass `requireAdmin` first. No public route, no cache headers that allow sharing (`cache-control: private, no-store`).
- Retention: deleted 30 days after the session ends by a daily sweep, and a Delete button on the research page. Not added to the off-site backup (a friend's private session; losing one is acceptable). Budget: 20 sessions × 25 MB = 0.5 GB of the 10 GB volume.

## Decision 3: the research page, smallest useful version
- `#/research` (admin only; others see "Only an admin can see research sessions"): a list of sessions, newest first: friend's name, date, length, size, whether a transcript exists.
- `#/research/<rsId>`: the replay on the left (rrweb `Replayer` in an iframe, the map snapshot painted over the canvas box), the transcript on the right (speaker, text, time from start). One timeline under the replay with play/pause, speed 1×/2×/4×, and markers from the action trail. Playing highlights and scrolls the current transcript line; clicking a line or a marker seeks the replay there.
- Later, not in this grant: notes on the timeline, export of a clip, a heatmap of clicks.

## The seam with Onboarding (their step 1)
1. `/api/me.researchSession`: `{id, status: "invited" | "consented" | "declined" | "ended", consentedAt}` for the friend's signed-in user; null for everyone else. Recording starts only on `consented` and stops on `ended`.
2. A server-side way to read the session: `world.research.get(id)` (or equal) giving the friend's user id and status, so the chunk route can check the writer.
3. The transcript lines (text guide and voice guide) stored with `{at: server ISO, speaker: "friend" | "guide", text}` per research session, readable by an admin route or a core function the research page can call.

## Plan (grant)
1. (M) Recorder and private store: core research-recordings store, the routes above, the client recorder gated on `researchSession`, map snapshots, the action trail, tests; measure a 20-minute mock session's size.
2. (M) The research page: list, player, transcript side by side, shared timeline, seek from a line; mock fixture with a recorded session.
3. (S) Live check and retention: a test research session through the test account on muster.town, the 30-day sweep, docs/research-mode.md.

Risk: rrweb 2.x is published as alpha; 1.1.3 is the last stable. Step 1 picks one and pins it.
