---
id: "dc_1qtsd3im07"
type: "report"
state: "building"
title: "Filing cabinet is now a file browser (folders by type, author filter) — 5c0aafd on main"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T16:19:58.649Z"
sessionId: "se_rx74d748s6"
assignmentId: "as_hny5f8fl2s"
costUsd: 1.2803028999999997
tokens: 2107881
turns: 40
createdAt: "2026-10-20T16:11:26.630Z"
updatedAt: "2026-10-20T16:19:58.649Z"
---
## What I did
I rebuilt the filing cabinet panel as a file browser and added type and author filters to the cabinet API, with a test. Typecheck passes and all tests pass (94+16+37+29+14). I pushed it straight to main as commit **5c0aafd** (rebased onto Root's commit 733193a, which moved the cabinet to the right wall). I didn't open a PR, per the workshop standing rule.

## Findings
- **API:** `GET /api/buildings/:id/cabinet?limit=&type=&authorId=` now returns `{docs, counts}`. `docs` is newest first and can be narrowed to one type and/or one author. `counts` is `[{type, authorId, n}]` for the whole cabinet; drafts and `fyi` are left out. Core gained `cabinetDocs(…, filter)` and `cabinetCounts`. An unknown type returns 400. The new test is in `packages/server/test/rest.test.ts` under "filing cabinet".
- **UI** (`packages/web/src/panels/Places.tsx`, `CabinetBrowser`):
  - There is one folder per doc type that has docs (Reports, Sources, Articles, Notes, Meeting notes, Requests, …), each showing its count.
  - An author dropdown lists everyone who has filed in that building, each with a total ("All authors (12)", "Ravi (6)", …). Picking an author changes every folder's count to that author's docs.
  - Opening a folder lists its docs newest first, up to the newest 200 (it says so if there are more).
  - Clicking a doc opens the existing doc viewer, whose back button returns to the folder.
  - The mock API and `docs/architecture.md` are updated, and there's a line in `docs/log.md`.
- **Checked in the running client:** I ran a real server on a throwaway seeded database (port 4400) with the Vite client in front of it, and drove headless Chromium against it. For the Carbon Cycle Lab cabinet:
  - Folders showed Reports 1, Sources 4, Articles 6, Notes 1.
  - The Articles folder listed 6 docs, newest first.
  - Picking Ingrid in the dropdown narrowed it to "Feedbacks & futures — desk article". Opening that doc showed the viewer with "← Articles" as the back button.
  - Back at the top level, still filtered to Ingrid, only "Articles 1" was left.
  - Screenshots are on my desk at `/tmp/vt/1-folders.png` through `5-root-filtered.png`. The test server is shut down.

## What I need from you
Nothing needed.
