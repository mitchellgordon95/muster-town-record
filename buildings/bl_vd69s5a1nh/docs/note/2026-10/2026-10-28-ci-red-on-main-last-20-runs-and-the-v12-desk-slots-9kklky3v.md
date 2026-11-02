---
id: "dc_l59kklky3v"
type: "note"
state: "building"
title: "CI red on main: last 20 runs, and the v12 desk_slots root cause (kr_cm5qb2wqh7)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["kr_cm5qb2wqh7","ci"]
createdAt: "2026-10-28T17:43:27.445Z"
updatedAt: "2026-10-28T17:43:27.445Z"
---
Exploration for kr_cm5qb2wqh7, 2026-10-28, main at 22dabd1. Data: `gh run list --branch main` and `gh run view --log-failed`.

## Headline
**None of the red runs in this window is a flake.** Each one is a deterministic break that was pushed to main, and each was fixed by a follow-up commit. **Zero re-runs:** none of the last 200 runs of the workflow has attempt > 1. So "no reruns" already holds. The KR is failing on "pass on the first attempt", and the cause is untested pushes to main, not test flakiness.

## Last 20 main runs (newest first)
| run | commit | attempt | result | failing test / error | fixed by |
|---|---|---|---|---|---|
| 40737284830 | 22dabd1 | 1 | success | | |
| 40737223652 | 158b50b | 1 | cancelled (concurrency) | | |
| 40737120330 | ced5d96 | 1 | cancelled | | |
| 40727911820 | 6af7714 | 1 | success | | |
| 40726345277 | 28fb84c | 1 | success | | |
| 40725526699 | e7fabc2 | 1 | success | | |
| 40640149902 | 4a4abd8 | 1 | success | | |
| 40638728502 | f8896de | 1 | success | | |
| 40637493888 | 9d86dde | 1 | **failure** | typecheck web: AgentPanel.tsx(237,269) TS2451 redeclare `isManager` (from fe85142) | f8896de |
| 40637173900 | fe85142 | 1 | **failure** | same TS2451 | f8896de |
| 40637030626 | a393c98 | 1 | cancelled | | |
| 40636775255 | e75a1ad | 1 | success | | |
| 40635362680 | 0c0650f | 1 | success | | |
| 40629794586 | 93e8ba3 | 1 | **failure** | web test/manual.test.ts "edition 1 … stays short": 1905 words, limit 1900 | 0c0650f |
| 40629044695 | 1eada04 | 1 | success | | |
| 40626777277 | d2b70e5 | 1 | success | | |
| 40618872228 | 6a93861 | 1 | success | | |
| 40618611509 | 1d0c6ba | 1 | **failure** | web test/manual.test.ts: 1921 words, limit 1900 | 6a93861 |
| 40618061912 | 2a3db42 | 1 | success | | |
| 40617690481 | d4fccbb | 1 | success | (the desk_slots fix) | |

Just before this window, the desk_slots episode:
| run | commit | attempt | result | error |
|---|---|---|---|---|
| 40614085621 | 2f39f71 | 1 | failure | core v12.test.ts: SqliteError: table desk_slots already exists |
| 40613854836 | b74358b (merge #65) | 1 | failure | many core tests: "[core] table docs is missing columns: topicOf" (two migrations numbered 050) |
| 40613660048 | 44e0451 | 1 | cancelled | |
| 40612811023 | 0e287b4 | 1 | failure | core v12.test.ts: SqliteError: table desk_slots already exists |
Main was red 01:04–01:53Z (~49 min, 3 failed runs). The prod gate in ci.yml (promote job) kept it from going live.

Window score: 4 failed of 20 (and 3 cancelled), so 13 of 20 are green on the first attempt if cancelled runs count as not-failed. Red episodes: desk_slots (Root, 0e287b4), duplicate 050 (merge of #65), manual word cap ×2 (Root, 1d0c6ba and 93e8ba3), web typecheck (Root, fe85142). Of the 5 red episodes, 4 came from direct pushes by Root (Workshop).

## Root cause: v12 "table desk_slots already exists"
- The test is in **packages/core/test/v12.test.ts** (the assignment said runtime; it's core). `v11Db()` (from line 44) seeds a DB with the **current** schema, then runs `DELETE FROM schema_version WHERE version >= 5` (line 61). It then undoes every migration from 005 to 051 by hand, with one DROP/ALTER line per migration (lines 62–~95).
- `migrate()` (packages/core/src/db.ts:21) re-applies every migration whose number isn't in schema_version. packages/core/migrations/050_desk_slots.sql:5 is a plain `CREATE TABLE desk_slots`. 0e287b4 added 050 but no matching `DROP TABLE desk_slots` in v11Db, so the replay hit an existing table.
- Of the four candidate causes, it's none of shared DB file, test ordering or a version-check gap. It is a non-idempotent migration meeting a hand-maintained undo list. **Deterministic, not a flake.**
- **Reproduced:** on main 22dabd1 I removed the `DROP TABLE desk_slots` line and got 3 of 3 runs failing with the same SqliteError. Restored, I got 3 of 3 passing (5/5 tests). The fix that's live is d4fccbb (Lena).
- **Will recur:** every new migration that creates a table or adds a column breaks v12.test.ts again until someone adds an undo line. The error points at the migration, not at the test.

## Proposed root fixes
| # | flake/break | root fix | where | owner | est. tokens |
|---|---|---|---|---|---|
| 1 | v12 undo list | Build the v1.1 DB forward instead of undoing: `migrate(db, dir)` already takes a dir, so copy migrations 001–004 to a temp dir, migrate, then insert the v1.1-shaped fixture rows with SQL. New migrations then never touch the test. | packages/core/test/v12.test.ts:44–~100 | Workshop (core tests); we could do it with their OK | 60–90k |
| 1b | (cheaper interim) | Guard test: every migration number ≥ 005 must appear as "added by NNN" in v11Db, failing with "migration 052 isn't undone in v11Db". Still red, but the message names the cause. | same file | Workshop | ~15k |
| 2 | push without running checks (4 of 5 episodes) | Repo pre-push hook running `npm run check:docs && npm run typecheck && npm test` (CI's check job takes ~1–2 min), installed by an npm `prepare` script that sets core.hooksPath. Desks that push straight to main get it on `npm ci`. | new .githooks/pre-push + root package.json | us (repo tooling, this KR) | 20–30k |
| 3 | duplicate migration numbers across merged PRs | The guard already exists (db.ts:31, from 2f39f71) with a test (2a3db42), but it fires only after the merge. Root fix: require PR branches to be up to date before merge (GitHub branch protection, which needs Mitchell), or a CI step that diffs migration numbers against origin/main. | .github/workflows/ci.yml or repo settings | us + Mitchell | ~10k (+ a setting) |
| 4 | manual word cap | Covered by #2. Optionally move the 1900-word check into check:docs so it fails in seconds. | packages/web/test/manual.test.ts:17 → scripts/check-doc-refs.ts | us | ~10k |

## Not investigated
The KR's example run 40454959781 (8a7a7ca, 2026-10-27, outside this window) is a **real timing flake**: runtime test/stale-state.test.ts "drain waits for facilitations": `expected "spy" to be called with arguments: [ 75 ]`, plus an unhandled "The database connection is not open" (the test closed the DB while the runtime was still running). It hasn't recurred in the last 45 main runs. Worth its own session.
