---
id: "dc_v8m9deefpl"
type: "report"
state: "building"
title: "Flag dc_4itg2gxfqf merged (02f1bbe, PR #115): Edit button on board notes; guest live check parked on deploy"
authorId: "ag_cbgc0tjdrb"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: flag dc_4itg2gxfqf merged as 02f1bbe (PR #115), redeploy queued; the guest live check is already parked on deploy 02f1bbe (as_qx54g0oemi). Rollup 31 Shipped candidate, not before ~20:10Z."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T18:02:46.931Z"
sessionId: "se_25xahjplv4"
assignmentId: "as_5smgvf1o9l"
costUsd: 1.1335464000000002
tokens: 56677
turns: 28
createdAt: "2026-10-30T18:00:43.630Z"
updatedAt: "2026-10-30T18:02:46.931Z"
---
## What I did
Built Mitchell's flag [dc_4itg2gxfqf](../../flag/2026-10/2026-10-30-can-i-get-an-edit-button-for-board-notes-please-tg2gxfqf.md) ("can i get an edit button for board notes please") as one PR, https://github.com/mitchellgordon95/muster-town/pull/115. It is merged to main as **02f1bbe** and a redeploy is queued. **02f1bbe should be live** after the restart. This session is parked until then, and the next one does the guest live check and takes the picture.

## Findings
- **Who can edit (core `canEditBoardNote` / `editBoardNote`, packages/core/src/verbs/docs.ts):** the note's author, a town admin, or a manager of the note's building. A lab's manager can't edit a Town Hall note. The existing write route only lets authors edit, so I added a minimal **PATCH /api/docs/:id** that takes a title and/or body and requires sign-in.
  - It only edits published board notes (type fyi).
  - It refuses an empty title or body.
  - It logs a doc.updated event, and only newly added @mentions send notifications.
- **Web (panels/Places.tsx `BoardNoteRow`):** every board note row has an Edit button. That covers the Town Hall board, each lab board's own notes and its Town-wide section. On the Town Hall board it sits next to "Take off the board".
  - Edit opens the title and body inline. Save calls the API and reloads the board with the new text; Cancel closes the form.
  - Guests and members without the right see no button.
  - The mock API has `editBoardNote` too.
- **Tests:**
  - core town-board.test.ts: author, manager and admin can edit; another member can't; a lab manager can't edit a Town Hall note; non-board docs and empty bodies are refused.
  - web townBoard.test.tsx: no button for a guest or a plain member, a button for a manager or admin, and the mock round-trip works.
  - Local runs all pass: typecheck, core 494/494, web 150/150, server 227/227. The repo has no CI checks.
- No migration, no Bank change.
- **Not done yet:** the guest live check (the panel still renders and has no Edit button) and the ≤300 px picture. The continuation does both once 02f1bbe is live.
- **Can't be done from a desk:** a real signed-in Edit and Save, because desks have no GitHub sign-in. Mitchell's "Your call" for rollup 31: edit one board note from the Workshop or Town Hall board and check the new text shows.
- Topic page: [dc_zxlu6zduyk](../../wiki/2026-10/2026-10-30-board-notes-edit-and-take-off-flag-dc-4itg2gxfqf-lu6zduyk.md).

## What I need from you
Nothing needed.
