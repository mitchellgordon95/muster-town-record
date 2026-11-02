---
id: "dc_gnq10nkhu9"
type: "report"
state: "building"
title: "PR #34: set the building's token budget when you create it (Settings already had it via #32)"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "merge, and then i'll follow up on the token distribution in a meeting"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:31:43.697Z"
sessionId: "se_b2qbbysc52"
assignmentId: "as_bul4t6ny42"
costUsd: 0.4218796
tokens: 22572
turns: 20
createdAt: "2026-10-20T04:28:08.793Z"
updatedAt: "2026-10-20T04:31:43.697Z"
---
## What I did
- Did what Mitchell asked: the building token budget can now be set both when a building is created and in its settings.
- Opened draft PR #34: https://github.com/mitchellgordon95/agent-town/pull/34. It builds on #32, which builds on #30.

## Findings
- **When you create a building:** the New building form on the Planning desk now has two fields:
  - **Max tokens / agent / day**, defaulting to 30M tokens.
  - **Daily pool (tokens)**, where empty means no limit.
  - The server API already accepted both values. Only the form was missing them. Code tests in #32 already cover creating a building with a pool and clearing it.
- **In building settings:** the building panel's Settings tab already has both fields, added in #32. Clearing the pool removes the limit, and raising either value resumes residents who were paused.
- **Checks:**
  - Typecheck passes.
  - `npm test`: 170/170 on the final run. One earlier run had a single failure in a core test (`verbs.test.ts`, about drafts and publishing). That test doesn't touch this change, and it passed when re-run.
  - The web build succeeds.
  - I didn't click through the form in a browser.
- **A gap this doesn't fix:** a new building starts with 0 tokens in its lifetime pot, which is filled only by donations. Its residents can't start work until someone donates, whatever the daily settings say. If "budget" should also mean a starting amount given at creation, that's a separate small change.

## What I need from you
Merge #30, then #32, then #34, and say whether new buildings should also get a starting token amount when they're created.

## Reply from Mitchell (2026-10-20 00:31)

merge, and then i'll follow up on the token distribution in a meeting

