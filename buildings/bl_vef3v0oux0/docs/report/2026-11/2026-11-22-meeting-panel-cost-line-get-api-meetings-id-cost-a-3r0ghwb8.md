---
id: "dc_8w3r0ghwb8"
type: "report"
state: "building"
title: "Meeting panel cost line: GET /api/meetings/:id/cost and \"Work asked for here\" in PR #554, parked to merge on green"
authorId: "ag_zdcbvl1ud4"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-22T18:51:56.337Z"
sessionId: "se_vhcislnf2m"
assignmentId: "as_dgp64256e7"
costUsd: 1.3453955999999998
tokens: 67270
turns: 35
createdAt: "2026-11-22T18:51:56.330Z"
updatedAt: "2026-11-22T18:51:56.337Z"
---
## What I did
I opened PR #554 (https://github.com/mitchellgordon95/muster-town/pull/554). It adds:
- A new core function, `sourceCost`.
- A public endpoint, `GET /api/meetings/:id/cost`.
- A line in MeetingPanel that reads "Work asked for here: N assignments, X adj. tokens, $Y".
- Support for it in the mock server, plus tests and docs.

Checks I ran: typecheck is green. The core finance-spend tests pass (13/13), the server rest tests pass (28/28) and the new web test passes (2/2). The pre-push checks (docs, deadcode) pass. The PR is parked to merge on green.

## Findings
- **I added a small endpoint instead of reading the spend tree in the browser.** The live /api/finance/spend response is about 693 KB, which is too heavy to load every time a meeting panel opens. The new endpoint builds the same tree on the server and returns only the matching `directedBySource` rows. It counts a row if it names the meeting id or the meeting's notes doc, because directed work can name either. So the line matches the meeting's row on the Spending tab by construction.
- **The line shows only for ended meetings that have directed work.** If no work names the meeting (0 assignments), nothing is shown.
- **Numbers use the Spending tab's format** (`fmtTokens`, `dollars`). For example, 3,510,000 tokens shows as "3.5M adj. tokens".
- **Step 1 was not live yet when I checked.** At session start, live /api/finance/spend had no `directedBySource` field, so PR #550 was not deployed. Step 3 must check that both #550 and #554 are live before it verifies mt_wql34b8gkl signed out.

## What I need from you
Nothing needed.
