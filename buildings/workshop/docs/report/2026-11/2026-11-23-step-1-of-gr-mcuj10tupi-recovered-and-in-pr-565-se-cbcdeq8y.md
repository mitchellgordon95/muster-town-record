---
id: "dc_l4cbcdeq8y"
type: "report"
state: "building"
title: "Step 1 of gr_mcuj10tupi recovered and in PR #565: Secretary runs no longer need the ranking schedule"
authorId: "ag_qtxdc7svca"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:19:21.078Z"
sessionId: "se_oj7ppa7yvr"
assignmentId: "as_mhxtuvtjnh"
costUsd: 1.2230534000000004
tokens: 61153
turns: 19
createdAt: "2026-11-23T16:19:20.985Z"
updatedAt: "2026-11-23T16:19:21.078Z"
---
## What I did
I recovered the dead session's code from the desk's auto-stash (stash@{0}, 22 Nov 18:58Z). It was never committed, and the old branch had no commits. I applied the stash onto current main. I renamed its migration from 128 to 129, because main now has 128_agents_daily_reset_index. Then I ran every check in the foreground under `timeout`, committed, pushed and opened PR #565 (https://github.com/mitchellgordon95/muster-town/pull/565).

## Findings
- **What the change does:** The Secretary's decision run (`afterDecision`), its backstop (`needsOverdue`) and "Rank now" (`pressRank`) no longer depend on the daily ranking schedule or its retainer.
  - Each one is now a run of the Town Hall's own job (jb_town-hall, rule building) on Fable, built by `townHallRun`.
  - Each run is capped at 40,000 tokens by the new `assignments.runCapTokens` (migration 129), which `watchRunCaps` reads.
  - The decision runs and the backstop runs are each capped at 8 a UTC day.
  - `ensureRankSchedule` no longer creates a schedule.
  - Docs updated: legible-delegation §6 and invariants/asks.
- **Checks, all passed:**
  - typecheck
  - core tests: 185 files, 1,147 tests (325 s)
  - server tests: 46 files, 372 tests
  - runtime tests: 36 files, 272 tests
  - web tests: 95 files, 477 tests
  - check:docs and knip (deadcode)
- **Why the last session hung:** No single test hung. `npm run check --fast` is just slow (core alone takes about 5.5 min), and the earlier session was waiting on a background monitor. Running each package's tests in the foreground under `timeout` works.
- **Key results:**
  - kr_tdfmc4lrpd: the backstop runs with no schedule once #565 is live. It stays open until the step 3 live check.
  - kr_d0yojmh6wv: the settle run after a decision is ungated (3-min debounce). Ranking a new ask within 15 min is step 2. It stays open.
- Topic page [dc_1r4r2xdvic](../../wiki/2026-11/2026-11-22-secretary-runs-on-events-gr-mcuj10tupi-4r2xdvic.md) is updated with the PR and the migration number.

## What I need from you
Nothing needed.
