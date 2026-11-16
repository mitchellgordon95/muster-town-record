---
id: "dc_t51ss5grl9"
type: "report"
state: "building"
title: "Operating manual book: PR #472 open, parked on CI"
authorId: "ag_rwiyrhlmj3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-16T18:20:23.828Z"
sessionId: "se_zmxk200q6e"
assignmentId: "as_jlt6x4fxrb"
costUsd: 2.0876799000000004
tokens: 104384
turns: 51
createdAt: "2026-11-16T18:20:23.799Z"
updatedAt: "2026-11-16T18:20:23.828Z"
---
## What I did
Built the operating manual as a book in the Town Hall, as Mitchell asked in meeting mt_dm14dgejml. PR https://github.com/mitchellgordon95/muster-town/pull/472 is a draft and is parked on CI.

## Findings
- **The book:** a new Town Hall furniture piece `manual` (TILE.BOOK = 38, drawn as a book open on a lectern). It sits at lot (7,2), just right of the library shelves, and is read from (7,3). On the live lot (x 68, y 4) that puts it at (75,6), read from (75,7). Its place `operating-manual` shows in `look` for everyone, and the help card has a line for it.
- **The click:** click or E calls `openOperatingManual`. That reads GET /api/operating-manual (live: [dc_hrmknv3j6q](../../../../../library/article/2026-11/2026-11-15-operating-manual-jobs-threads-and-asks-mknv3j6q.md)) and opens the doc as a sheet. If the town has no manual yet, it opens the library panel instead.
- **Docs:** docs/manual.md now names the book. I trimmed the Town health wording to keep the file at 1900/1900 words. I also updated architecture.md and added a docs/log.d entry.
- **Verified:**
  - typecheck passes and check:docs passes.
  - The web suite passes (85 files, 421 tests), plus the new test/operatingManualBook.test.ts (2 tests).
  - 4 core layout test files pass (43 tests), including the new furniture test for the place, tile and path.
  - The full core suite was still running when I parked, so CI is the full check.
- **Next session:** if CI is green, mark the PR ready and merge it, with no redeploy. When /api/health shows the merge sha, check the place and tile in /api/town.

## What I need from you
Nothing needed.
