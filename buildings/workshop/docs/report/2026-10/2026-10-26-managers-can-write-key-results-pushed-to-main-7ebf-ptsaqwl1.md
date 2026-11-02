---
id: "dc_g0ptsaqwl1"
type: "report"
state: "building"
title: "Managers can write key results: pushed to main 7ebf5ab; parked for the live check"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: 7ebf5ab (manager-writable KRs, set_key_result, migration 033, kr.created/updated with actor, rollup \"Key results I wrote\" section) is pushed and your continuation verifies it live. Pix takes the next step (write the Workshop KR from dc_qg2gppz9jd, propose the Bank grant dc_2uqmfdittg) as its own assignment waiting on deploy 7ebf5ab."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T15:33:07.684Z"
sessionId: "se_3tyx9wfoh8"
assignmentId: "as_6kwwuh4ct6"
costUsd: 2.6663097999999996
tokens: 167708
turns: 59
createdAt: "2026-10-26T15:32:20.684Z"
updatedAt: "2026-10-26T15:33:07.684Z"
---
## What I did
Built all four scope items from the 1:1 (mt_ayi4y9ybyj), committed straight to main as **7ebf5ab**, pushed it and requested a redeploy. The work is parked until 7ebf5ab is live, then I verify it.

## Findings
- **Who can write key results:** a building's own manager agent (the agent in `buildings.managerAgentId`) can now create and edit key results on its building's goal. Other agents are refused, and so is a manager on another building. Humans keep every power. Deleting a key result and marking it met or missed are still human-only, and a manager can still set status only up to claimed. The code is `requireWriter` and `requireHuman` in `core/src/grants.ts`.
- **New tool `set_key_result`:** `buildingId` defaults to the manager's own building; pass `id` to edit an existing key result. The other fields are `text`, `howToCheck` (the measure) and `sourceDocIds` (the meeting notes or report it comes from). `sourceDocIds` is required for a new key result and must point at published docs. The tool uses the same core path as `POST /api/buildings/:id/key-results` and `PATCH /api/key-results/:id`.
- **Database:** migration 033 adds `createdBy`, `editedBy` and `sourceDocIds` to each key result. The API view also returns `createdByName` and `editedByName`.
- **Events:** `kr.created` and `kr.updated` record who did it (`agentId`, `payload.by`, `payload.byKind`), whether the words changed (`payload.edited`) and the new words.
- **Rollup listing:** when a manager submits its next rollup, a "## Key results I wrote" section is added automatically. It lists each key result the manager created or edited since its last rollup, with id, text, how to check and sources, so Mitchell can keep or cut it. A rollup carrying such a list doesn't need covered reports. The manager's in-tray prompt lists these key results too.
- **Prompts:** the manager prompts and the blocked-building assignment now say "settle key results in a 1:1 or meeting, then `set_key_result`" instead of "only a human writes them".
- **Web:** under each key result, Building → Settings → Key results shows "Written by X, edited by Y" and links to its source docs. The text on the board and the blocked banner (`UNBLOCK_LINE`) was updated to match.
- **Docs:** `docs/goal-directed-budgets.md` has a new "Managers write key results" entry in the model change section.
- **Verification so far (local only):** `npm run typecheck` is clean, and the core (265), runtime (119), server (67) and web (55) test suites all pass. New tests are in `core/test/kr-authors.test.ts` (permissions, events with the actor, rollup listing) plus an author-line test in the web package. Nothing is checked live yet.
- **Not done yet:** Pix writing the Workshop key result from [dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md) and proposing the Bank grant ([dc_2uqmfdittg](../../note/2026-10/2026-10-26-bank-accuracy-what-the-bank-counts-today-the-real-qmfdittg.md)). That has to wait until 7ebf5ab is live.

## What I need from you
Nothing needed.
