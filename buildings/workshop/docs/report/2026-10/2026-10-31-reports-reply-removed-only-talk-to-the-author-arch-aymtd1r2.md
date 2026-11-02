---
id: "dc_3daymtd1r2"
type: "report"
state: "building"
title: "Reports: Reply removed, only Talk to the author + Archive (PR #134 merged as dbff17e); live check parked"
authorId: "ag_e0timon0jt"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #134 dbff17e: Reply gone from reports, Talk to the author + Archive only, /reply 404, directed source \"rollup a human replied to\" removed. Live check already queued (as_11xxb6jx2o, waits on deploy dbff17e); signed-in crop for rollup 34 comes from that session."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T01:17:37.645Z"
sessionId: "se_vo0qza1bsv"
assignmentId: "as_y0ygoewah9"
costUsd: 1.8410639000000004
tokens: 92053
turns: 36
createdAt: "2026-10-31T01:15:24.575Z"
updatedAt: "2026-10-31T01:17:37.645Z"
---
## What I did
Removed the Reply option from reports (Mitchell, 1:1 mt_cz11aqe81a). PR https://github.com/mitchellgordon95/muster-town/pull/134 is green in CI and merged to main as **dbff17e**, and a redeploy is queued. The live check is parked until dbff17e is live.

## Findings
- **Web:** `ReplyBox` is gone, along with its textarea and the "merge" reply. A pending report now has exactly two actions:
  - **Talk to <author>**: the existing 1:1 button, unchanged.
  - **Archive**: a new `ArchiveButton`.
  These two show in the doc reader the in-tray opens (rollups, checkpoint and close reports, lab in-trays) and on the review deck's report slide (`ReportActions`, plus "Open the report"). A report that already has a decision shows no Archive. Archiving on a deck slide still advances to the next slide.
- **Archive behaves like the old empty reply.** `POST /api/docs/:id/archive` sets decision "approve" with no note and creates no assignment. It still carries `deckSlide`/`meetingId` and records a meeting decision "<name> archived dc_… (on slide n)". The Bank, grants, checkpoints and `waitFor {decision}` all behave as before.
- **Server:** `POST /api/docs/:id/reply` is removed (the test asserts 404). Core `reply.ts` (`replyToReport`, the merge-reply instruction) is replaced by `archive.ts` `archiveReport`.
- **Directed lane:** "a rollup a human replied to" is no longer a valid source. I removed it from `humanSource` (lanes.ts), the manager prompt, and the schema `sourceId` description.
- **Docs updated:** manual.md, architecture.md, meetings.md, multimedia.md, waterfall.md, README, a superseded note on design review 4, and a line in docs/log.md.
- **Left unchanged:** grant Fund/Counter/Reject, goal proposals, flags (FlagDecideBox), the outbox and the manager's `review` tool. Old reports that were replied to before this change still show the "replied" pill and the "replied to" history line.
- **Tests:** typecheck, check:docs and knip are clean. web has 165 tests, core 514, server 225, all passing. There is one new test (web/test/talkToAuthor.test.tsx): a pending report in the in-tray reader and on a deck slide renders Talk to Lena and Archive, with no Reply and no textarea; a decided report shows no Archive.
- **Plan for the continuation:**
  1. Confirm that `GET /api/health` reports a commit containing dbff17e.
  2. As a guest, check that the Town Hall in-tray renders, `/api/review-deck` returns 200, and `POST /api/docs/<id>/reply` returns 404.
  3. Take one ≤300 px crop (mf_) of a report card showing the two buttons. A guest can't see Talk to/Archive, so this needs a local dev server signed in as admin (method in [dc_vrrph0d7ss](../../wiki/2026-10/2026-10-28-talk-to-the-author-1-1-docs-and-grants-rph0d7ss.md)).
  4. Update the topic pages [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md) and [dc_vrrph0d7ss](../../wiki/2026-10/2026-10-28-talk-to-the-author-1-1-docs-and-grants-rph0d7ss.md).

## What I need from you
Nothing needed.
