---
id: "dc_2tk022u655"
type: "report"
state: "building"
title: "Acknowledge from the Reports row: PR #8 (stacked on #3)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":["https://github.com/mitchellgordon95/agent-town/pull/8"]}
tags: []
verdict: "continue"
decision: "stop"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T01:54:50.336Z"
sessionId: "se_ijuq2swxb5"
assignmentId: "as_r8z0mfqa1m"
createdAt: "2026-10-20T01:53:42.122Z"
updatedAt: "2026-10-20T01:54:50.336Z"
---
## Summary
Done. Draft PR https://github.com/mitchellgordon95/agent-town/pull/8.

Reviewers now get a one-click **Acknowledge** button on pending rows in the agent panel's Reports tab. It only shows when `store.can("building.review", homeBuildingId)` is true, and it sends `decision: "approve"`, which creates no assignment. Continue, Redirect and Stop still happen at the in-tray, because they need the proposal or a note.

I checked it in a real browser (headless Chromium against the Vite mock). The PR description notes that reports written before #2 show no turns.

While merging #3's branch onto v1.2 main I found a migration-numbering problem in #2: its 004 will never run on live databases.

## What I did
- **Stacked on #3:** merged its branch onto current main (v1.2) and resolved two conflicts:
  - `docs/log.md`: kept both sides.
  - `runtime/test/work.test.ts`: kept v1.2's `idle` status plus #2's usage-stamp assertions.
- **The change:** `ReportsTab` in `packages/web/src/panels/AgentPanel.tsx`.
  - A `.doc-row-act` flex wrapper holds the row and the button, so no button sits inside another.
  - After a click, the decision goes into the store via `putDocs`, a toast shows, and the list reloads.
  - 2 CSS lines and a log line.
- **Verified:**
  - `npm run typecheck`: clean.
  - `npm test`: all packages pass (web 3/3, core 56, plus the others).
- **Browser check:** I set up Playwright with Chromium, pulling the missing system libraries from Debian .debs into ~/tools because there's no root. Results:
  - **Reviewer:** 1 button. After the click the pill reads *acknowledged* and the button is gone.
  - **`?as=visitor`:** 0 buttons.
  - **390px mobile:** the row wraps cleanly and the button doesn't overflow.

## Findings
- **The feature works as specified.** The screenshots are described in the PR.
- **Bug in #2 (not this PR):** main jumped from migration 003 to 005_v12 and 006_mentions. `migrate()` skips any file with `n <= current`, so on a live database already at version 6, #2's `004_doc_turns.sql` never runs and `docs.turns` won't exist. Fresh databases are fine. I've told Root it probably needs renumbering to 007.
- **Older reports show no turns.** Fixture and older reports have no `turns`, so rows show only `$x · N tokens`. This is expected.

## Proposal for next session
Should the in-tray rows (Places.tsx `IntrayRow`) get the same inline Acknowledge, so that the in-tray handles routine reports in one click and only opens a report for Continue, Redirect or Stop?
- **Why:** it means fewer clicks for the most common decision.
- **Sources:** the existing `ReviewBox` and `IntrayRow`.
- **What would change the plan:** if the manager wants every decision made with the report open.

## For others
- @Root: renumber migration 004 in PR #2 (see Findings).
- The review queue is now stacked 4 deep: #1 → #2 → #3 → #8. Merging #1–#3 first keeps #8's diff to one commit.
- Browser-check recipe for desks: `~/tools/shot.py` with `LD_LIBRARY_PATH` read from `~/tools/ldpath`. It opens a panel with `await import('/src/state.ts')` and then `store.open(...)`.

## Questions for humans
- Can the desk image ship Chromium's system libraries (libnss3 and friends), so browser checks don't need this workaround?
