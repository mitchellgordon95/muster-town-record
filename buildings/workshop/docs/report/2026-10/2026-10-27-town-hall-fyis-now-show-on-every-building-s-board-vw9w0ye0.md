---
id: "dc_f7vw9w0ye0"
type: "report"
state: "building"
title: "Town Hall FYIs now show on every building's board (1ece19a on main, redeploy queued); parked to copy the rules once it's live"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Town Hall board items 1-4 on main as 1ece19a; continuation resumes when it is live. Item 5 correction agreed: post the Workshop standing rules (commit straight to main; pull main and restart after committing) as the Town Hall FYI. If the post is refused for lack of building.manage, say so in your report and I will post it as manager."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T23:29:49.863Z"
sessionId: "se_2lpwaylhrv"
assignmentId: "as_1ep1fqj472"
costUsd: 2.0604622000000004
tokens: 103023
turns: 61
createdAt: "2026-10-27T23:27:38.515Z"
updatedAt: "2026-10-27T23:29:49.863Z"
---
## What I did
Built items 1–4 of town hall mt_q1w4o85ao9, decision 5 item 2. Pushed straight to main as **1ece19a** (rebased onto Keel's forks step 2, dde6f86) and queued a redeploy. Once 1ece19a is live this parks and resumes for item 5.

## Findings
- **Board (1):** the `board` verb and `GET /api/buildings/:id/board` now list the Town Hall's FYIs first, then the building's own FYIs. Each Town Hall FYI carries `townWide: true`, and the verb also adds `from: "Town Hall"`. The Town Hall's own board doesn't list them twice. The code is `boardWithTownDocs` in core/src/verbs/docs.ts.
- **Web (2):** the board panel shows a "Town-wide" section above the standing rules and the building's FYIs. The section is hidden when the Town Hall board is empty. The mock server does the same.
- **Brief (3):** every work session's brief has a "Town-wide FYIs" block (`townBoardBlock`, through `sessionMemory`) just before the standing rules. This covers desk, host and manager sessions. No block is added when the Town Hall board is empty.
- **Posting (4):** `write` takes `buildingId`, for FYIs only. Posting an FYI with state building to `town-hall` is allowed for town admins and for anyone with `building.manage` on any building. Everyone else gets 403. The same works for humans via `POST /api/docs`.
- **Tests:** new test core/test/town-board.test.ts. Typecheck is clean across all packages. The core tests for town-board, rules-board, prompts, manual-seed, verbs, mentions and forks pass, and so does the web manual test.
  - The full `npm test` hit the 30-minute background limit on this desk, so I didn't run the whole suite.
  - One memory.test.ts failure under load passed when rerun on its own.
- **Docs:** updated the manual, docs/architecture.md and PAST_MANUAL_EDITIONS (added edition 3.4, c3b6e98). The manual is now 1898 words against its cap of under 1900.
- **Item 5 needs a correction:** the Workshop board has no FYI docs (`board` returns `docs: []`). The merge rules Mitchell meant are the Workshop's **standing rules**: "commit straight to main; pull main and restart after committing". Next session I'll post that text to the Town Hall board as an FYI. My agent may not have `building.manage`; if the post is refused, I'll ask Pix to post it. Then I'll confirm the Bank Transparency board (bl_vef3v0oux0) shows it as townWide.

## What I need from you
Nothing needed. This resumes by itself when 1ece19a is live.
