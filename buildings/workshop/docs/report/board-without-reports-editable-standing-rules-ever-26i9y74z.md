---
id: "dc_cf26i9y74z"
type: "report"
state: "building"
title: "Board without reports + editable standing rules every session starts with (draft PR #16)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:18:37.560Z"
sessionId: "se_vtm2m1kmdx"
assignmentId: "as_tq118htkoh"
createdAt: "2026-10-20T02:09:41.307Z"
updatedAt: "2026-10-20T03:18:37.560Z"
---
## Summary
Both are done, in draft PR https://github.com/mitchellgordon95/agent-town/pull/16. I made the change across the whole stack, as you asked in your interrupt.
- **Reports are off the building board.** That applies to the `board` tool agents use, the REST endpoint and the web panel. Reports live only in the in-tray, and `search` with type "report" still finds them.
- **Standing rules.** Each building has a `rules` text (markdown). You edit it on a gold note pinned to the top of the board: walk to the board, press E, click **Edit** or **Add rules**, then **Save rules**. The rules are added to the system prompt of every session in that building: work, reviewer and meeting facilitation. Edits take effect from the next session. Only holders of `building.manage` can edit; everyone else just sees the note.
- **Side fix:** migrations now run if their number hasn't been recorded yet, instead of only when they're above the highest applied number. Without this, Root's `004_doc_turns.sql` (#2) would be silently skipped on existing databases.

## What I did
- schema: `Building.rules` (string, max 8000 characters, default ""), added to Create/UpdateBuildingInput. Board verb description updated.
- core: migration `008_rules.sql`. `prompts.standingRules()` is added to `workSystemPrompt`, `reviewSystemPrompt` and `facilitateSystemPrompt`. WORLD_RULES now says the board holds articles, notes and meeting notes, and that reports go to the in-tray. The board query excludes reports. `migrate()` now applies by set.
- server: the `/board` route excludes reports. Corrected the in-tray route comment.
- web: `StandingRules` card in `BoardPanel` (Places.tsx) with gold note styling. New subtitle: "Standing rules, articles and notes. Reports go to the in-tray." The mock server and fixtures now support rules, and the Workshop fixture has sample rules.
- docs: README, an architecture.md section on standing rules (plus the board definition), and a log line.
- Told @Root that #16 makes their 004→007 renumbering unnecessary.

## Findings / verification
- `npm run typecheck`: passes in all packages. `npm test`: everything passes (core 59, plus 20 / 26 / 23 in the other packages). `npm run build`: passes.
- New `packages/core/test/rules-board.test.ts` checks:
  - the board leaves out a fresh report, which is still in the in-tray
  - a manager's rules appear in the work and review prompts
  - a member gets forbidden
  - blank rules add nothing to the prompt
  - a lower-numbered migration added later still applies, and migrate is idempotent
- I updated the v1.1 → v1.2 migration test: its simulated old database now drops the `rules` column too.
- No real screenshot: headless Chromium in my desk is missing `libnspr4.so`. The PR has a text description of the screen instead.

What I don't know: whether you wanted **town-wide** rules (one text for every building) rather than per-building ones. I built per-building rules because each building keeps its own policies and the board is per building. Adding a town-level `rules` to `Town` (shown in Town Hall) would be a small follow-up if that's what you meant.

## Proposal for next session
Add the attendee multi-select to the "Call meeting" form (BuildingPanel MeetingsTab and MeetingPanel's empty-room button), wired to `attendeeIds` from Root's PR #10.
Why: you asked to choose who attends; Root built the server side and asked me for the UI. Source: Root's report dc_2w2xo9uh1i and their tell. If you want town-wide standing rules first, do that instead.

## For others
- @Root: once #16 lands, migrations apply by set, so 004 in #2 is fine as-is. Don't use 008.
- Everyone: the board no longer shows reports. Use `search` with type "report" to read colleagues' reports, or the in-tray.
- Collective configs can't set rules at seed yet (no `rules` in CollectiveBuildingSpec). It's UI/PATCH only.

## Questions for humans
- Per-building rules (built) or one town-wide set as well?
- Should I add the Chromium libraries (libnspr4, libnss3) to the desk image so web PRs can include real screenshots?
