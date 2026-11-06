---
id: "dc_wnxj1ug5ce"
type: "report"
state: "building"
title: "Weekly check-timing watch: slowdown alarm tripped (test suite growth)"
authorId: "ag_k19cutyg02"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_87kealnkye","dc_r5j4bdtmzo"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: the agreed trigger (dc_r5j4bdtmzo decision note, dc_dbrkeiac5r) has fired, so I'm re-proposing a build-time grant now. Scope: the fix, not the history page. PR #247 (schema image, −19% at 76 migrations; main now carries 96 files in packages/core/migrations, so every openDb at core/src/db.ts:14-25 replays 96 of them per test DB and the saving is larger) plus the one-root-vitest-run lever (scripts/check.ts:46 runs six sequential workspace runs), then a 10-run verification. The history page stays rejected (gr_xurio0oki5, twice): the retainer watch sc_5qs03u3172 already does the observing job and tripped without it. The sc_45pi8pvl9q → retainer re-creation was done last session (sc_5qs03u3172, in the Town Hall in-tray)."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-06T06:04:04.515Z"
sessionId: "se_n8buu7yj7n"
assignmentId: "as_ihd1gnzwq3"
costUsd: 0.02419209
tokens: 1210
turns: 9
createdAt: "2026-11-06T06:02:45.566Z"
updatedAt: "2026-11-06T06:04:04.515Z"
---
## What I did
Pulled the `check:` timing line and GitHub job duration from the last 12 green CI runs on main (2026-11-05 22:33Z to 2026-11-06 05:06Z; run ids 42122431486 … 42166369737). Compared medians and ranges to the 2026-10-30 baseline ([dc_r5j4bdtmzo](../2026-10/2026-10-30-kr-8wilbokqcn-exploration-the-timing-line-already-j4bdtmzo.md)). Rewrote the "Build times / fast check" topic page ([dc_87kealnkye](../../wiki/2026-10/2026-10-29-build-times-fast-check-kealnkye.md)) with this week's numbers. No code changes, no PR.

## Findings
Seconds, median (range), 12 green main runs:

| Step | This week | Baseline 10-30 | Ratio |
|---|---|---|---|
| docs | 0.5 (0–1) | 0 (0–1) | — |
| deadcode | 4.5 (3–6) | 3.5 (3–5) | 1.3× |
| typecheck | 16 (12–22) | 13.5 (10–18) | 1.2× |
| tests | 158 (109–191) | 76.5 (58–93) | 2.1× |
| check total | 180 (124–219) | 94 (73–116) | 1.9× |
| whole job | 201 (141–243) | 113 (89–136) | 1.8× |

**Alarm tripped.** Median total is 180 s (threshold 140 s). Tests median is 2.07× baseline (threshold 2×). Six of 12 runs exceed 180 s (184, 196, 215, 217, 219, 219). Note the first slow run is 42123347058 (22:39Z 11-05), with 42122431486 (22:33Z) at 2m04 just before it.

**Likely driver (not isolated):** the test suite grew. Test cases went 1,278 (af85f2a, 11-01) to 1,705 (1bbaf18, 11-05), +33%; test files 211 to 284. Between the fast and slow run the commits touch only `scripts/delight-walk.mjs`, so no single commit explains the step. Two fast runs (2m04, 2m06) are unexplained; runner variance is about 1.6× on identical code.

Next session: find when the test-case count crossed ~1,400 (e.g. `git grep -c` per commit on main) to date the growth, and measure per-workspace vitest time to see whether one workspace dominates.

## Proposal for next session
Verdict stop for this watch. The alarm is real, so a follow-up is needed (see What I need). The levers already measured: PR #247 (test-db schema image, −19% server time, draft, green on branch) and vitest `projects` in one root run (unmeasured, scripts/check.ts:46).

## What I need from you
Ask Mara to propose the history-page grant (the no-commit annotation design in [dc_r5j4bdtmzo](../2026-10/2026-10-30-kr-8wilbokqcn-exploration-the-timing-line-already-j4bdtmzo.md), ~40–60k tokens, one PR) and/or a fix: merge or fast-track PR #247 and measure the vitest-projects lever. Also note that the schedule sc_45pi8pvl9q ended; the repeat must be re-created as a retainer from 2026-11-13 pending Mitchell's approval.
