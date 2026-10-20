---
id: "dc_8nhfvwom6a"
type: "report"
state: "building"
title: "Browser checks: #14, #16 and #17 pass; #15 can't be seen in a browser; found a summary bug (draft PR #23)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_5iamj6wpfl"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/23"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "merge"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:52:43.902Z"
sessionId: "se_qrgbsrn3ee"
assignmentId: "as_4at5jpjuxg"
costUsd: 1.1431221999999999
tokens: 2630086
turns: 51
createdAt: "2026-10-20T03:45:54.372Z"
updatedAt: "2026-10-20T03:52:43.902Z"
---
## What I did
- Installed Chromium without root using Pix's recipe (dc_5iamj6wpfl) and drove the UI with Playwright.
- Ran it against a real local server on main (adb181c): workshop collective, temporary data directory, ANTHROPIC_API_KEY removed, so no agent sessions could spend money.
- Shut both servers down afterwards.

## Findings
- **#14 (call another meeting after one finishes): passes.** I ran call → end twice from the Town Workshop room. Each time the empty room showed "Call a standup" and "Last meeting: … (done, just now)". A finished meeting shows "Call another standup", and clicking it opens a new meeting in collecting. After ending a meeting and reloading the page, the room shows "Call a standup" again. One small gap: after a reload the "Last meeting" link is missing, because the snapshot only carries live meetings. That matches what the PR says it does.
- **#17 (residents without titles): passes.** Planning desk → Residents → New resident asks only for a name and sprite. "Newbie" was created with title "" and direction "". To test an existing agent, I created "Oldtimer" through the API with title "Backend engineer" and direction "Only touch the backend.". Neither text appears anywhere I checked: agent panel subtitle ("resident · Town Workshop"), Members tab, building panel, meeting room, planning desk, or the map prompt ("Talk to Oldtimer"). Service agents keep their roles.
- **#16 (reports off the board, standing rules): passes.** I put one `report` doc in the workshop with state "building" (inserted straight into the database, since humans can't create reports). `GET /api/buildings/workshop/board` and the board panel both leave it out; the note and meeting notes still show. On the board panel, "Add rules" → Save works, and the rules are still there after a reload. That rules actually reach session prompts is covered only by #16's unit tests; I didn't check it in a running session.
- **#15 (prompts with no titles, lanes or forced next step):** prompt text only, so there is nothing to see in a browser. `packages/core/src/prompts.ts` has no remaining `agent.title`, `.direction` or "Proposal for next" references.
- **Bug found and fixed in draft PR #23:** https://github.com/mitchellgordon95/agent-town/pull/23
  - With no API key, every attendee's standup summary read "Not logged in · Please run /login". `summarize` (`packages/runtime/src/meetings.ts`) posted the text of a failed call as the summary.
  - It now posts a summary only when the call succeeded. The session still ends with status error.
  - A new test fails without the fix and passes with it.
  - `npm run typecheck` passes and `npm test` passes all 158 tests.
  - The PR also adds a line to docs/log.md.

## What I need from you
Review and merge PR #23.

## Reply from Mitchell (2026-10-19 23:52)

merge

