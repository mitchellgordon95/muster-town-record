---
id: "dc_qefnwr058y"
type: "report"
state: "building"
title: "Bulletin board read/unread per human + red badge (PR #368); parked on CI"
authorId: "ag_va3f9qees9"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_04q4h8s229","dc_rndlibet31","dc_52njv3shp8"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/368"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The continuation (as_xryg315zhb, waiting on PR #368's CI) already covers merge + live check, so nothing more to queue. Will fold into the next rollup once #368 is live and verified."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-05T20:28:25.653Z"
sessionId: "se_s3qynccvn1"
assignmentId: "as_smkhxsbm7j"
costUsd: 2.4865745000000006
tokens: 124329
turns: 68
createdAt: "2026-11-05T20:28:17.339Z"
updatedAt: "2026-11-05T20:28:25.653Z"
---
## What I did
Built Mitchell's flag [dc_04q4h8s229](../../flag/2026-11/2026-11-05-nit-can-i-get-a-read-unread-tracker-for-the-bullet-q4h8s229.md) (read/unread tracker on the bulletin board for each user, plus a red badge for unread notes) as one draft PR: https://github.com/mitchellgordon95/muster-town/pull/368. I'm parked until its CI finishes. Then I merge if it's green, with no redeploy (CI deploys main), and check it live.

## Findings
- **Server:** migration 094 adds a table `bulletin_reads(userId, docId, readAt)`. For a signed-in human, `GET /api/bulletin` now marks each note `unread` true or false and returns an `unread` count. Guests and agents get the notes with no flags. `POST /api/bulletin/:id/read` or `/api/bulletin/all/read` marks notes read and returns `{unread}`. I put this route on the list of actions allowed before an admin lets someone in, because marking a note read is reading, not taking part.
- **Rule I chose:** your own notes count as read. A read is tied to the note's id and is never deleted, so a note taken down and pinned again stays read, even if it was edited.
- **Panel:** unread rows get a red "new" pill, and opening a note marks it read. Above the list there's a line "N new notes since you last looked" with a "Mark all read" button.
- **Map:** the bulletin board shows a red count badge, the same style as the in-tray badges. It only appears for a signed-in human with unread notes. The count comes from the existing `/api/bulletin` fetch, which reloads on connect, when a note is pinned or taken down, and when the signed-in user changes. No new poll was added.
- **Checks:** `npm run typecheck` passes. The server bulletin tests pass (2), and so do the web bulletin tests (5) and the full web suite (343). Core migration and export tests pass, and `check:css` reports 0 stray values. In the mock, in Chromium at 1280×800: the board shows a badge "1", and opening the note brings the count to 0.
- **Not checked:** nothing has been tried on live yet; that happens after the merge.
- **Picture:** ![Bulletin board unread badge](/api/media/mf_pb2wf81mje.png). In the mock, the seeded note's author shows as the raw id "us_ada", because the mock has no avatar for that user. Live notes by real users show their names.
- Topic page "Bulletin board": [dc_rndlibet31](../../wiki/2026-11/2026-11-05-bulletin-board-dlibet31.md).

## What I need from you
Nothing needed.
