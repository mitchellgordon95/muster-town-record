---
id: "dc_zxlu6zduyk"
type: "wiki"
state: "building"
title: "Board notes: edit and take off (flag dc_4itg2gxfqf)"
authorId: "ag_cbgc0tjdrb"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-10-30T18:00:30.420Z"
updatedAt: "2026-10-30T18:10:46.269Z"
---
State on 2026-10-30 ~18:12 UTC. Source: Mitchell's flag [dc_4itg2gxfqf](../../flag/2026-10/2026-10-30-can-i-get-an-edit-button-for-board-notes-please-tg2gxfqf.md) ("can i get an edit button for board notes please"), assignments as_5smgvf1o9l (build, report [dc_v8m9deefpl](../../report/2026-10/2026-10-30-flag-dc-4itg2gxfqf-merged-02f1bbe-pr-115-edit-butt-m9deefpl.md)) and as_qx54g0oemi (guest live check).
- LIVE as 02f1bbe (PR #115). /api/health commit 02f1bbe at 18:06Z. Guest live check done 18:10Z: Workshop board (Town-wide section + own notes) and Town Hall board both render; 0 Edit buttons and 0 "Take off the board" for a guest. Picture mf_w59dl2rc40 (375x300, Workshop board panel).
- core verbs/docs.ts: `canEditBoardNote(world, me, doc)` = author, town admin, or building.manage on the note's buildingId (a lab's manager can't edit a Town Hall note). `editBoardNote(world, me, id, {title?, body?})`: published FYIs only (state building, BOARD_TYPES), trims, refuses empty title/body, appends doc.updated, notifies only new @mentions.
- server: PATCH /api/docs/:id {title?, body?} (requireAuth). POST /api/docs (write verb) is still author-only.
- web panels/Places.tsx: `BoardNoteRow` renders each board row with Edit (when DocList gets onEdited and `canEditBoardNote`, a client mirror) and Take off the board (Town Hall only, `canUnpublish`). Edit opens title+body inline; Save → api().editBoardNote → board.reload. Mock: MockApi.editBoardNote.
- Tests: core test/town-board.test.ts, web test/townBoard.test.tsx.
- Not exercised by any agent: a real signed-in Edit/Save (desks have no GitHub sign-in). Mitchell's "Your call" in rollup 31.
- How to reach the boards as a guest in headless Chromium: /workshop/, "Watch first", click the Workshop corkboard on the back wall; for Town Hall click it on the minimap, walk up 8× ArrowUp, click the corkboard on the back wall.
