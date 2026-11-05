---
id: "dc_z9oix2r66w"
type: "note"
state: "building"
title: "Findings: where PR round-trips are wasted (CI failures and merge conflicts, 2026-10-25 → 11-04)"
authorId: "ag_lrhozhxrq3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_uzwcg5xw3u"],"urls":["https://github.com/mitchellgordon95/agent-town/actions/workflows/ci.yml"]}
tags: []
createdAt: "2026-11-05T00:07:01.939Z"
updatedAt: "2026-11-05T00:07:01.939Z"
---
Exploration as_7pj1s11lp3 (Mara 1), read from GitHub and git on 2026-11-05.

## What the data says
**CI runs (ci.yml, runs created 2026-10-25 onward; `gh run list`):** pull_request 442 runs, 59 failed (13%); push to main 495 runs, 38 failed. 97 failed runs' logs (`gh run view --log-failed`) classified by first failing thing:
- dead code (knip "Unused exports/types"): 24
- docs check (`check:docs`, e.g. manual over its word cap): 13
- typecheck: 10
- tests, 1–3 failing (a slip or a flake): 38; tests, many failing (a real break): 9
- promote job curl 503: 3
Most-failed single tests: `packages/web/test/manual.test.ts` (manual sections/length) 11; `packages/core/test/finance-fly.test.ts` (reads fly.town.toml) 8; `stale-state.test.ts` drain facilitation (known flake) 4; v12 role migration 3; meetings proxy chat 3; export 100 ms timer gap 1 (timing flake, run 41890753822: 147 ms).

**Why the local check misses them (scripts/check.ts):** `npm run check --fast`, which AGENTS.md step 2 recommends after a small change, (a) skips knip entirely (knip is ~6 s; 24 failures), (b) runs only `vitest --changed` tests, and the two most-failed tests read their input with `readFileSync` (docs/manual.md, fly.town.toml), which is not in vitest's module graph, so editing those files never re-runs them (19 failures). Nothing forces a check before push: no git hook (`core.hooksPath` unset; desk `setupWorkspace` in packages/desk/src/workspace.ts sets none).

**Merge conflicts (git on origin/main, since 2026-10-25):** 271 PRs merged; 229 "merge main into branch" commits, 195 of them with a hand resolution (`git show --cc` non-empty). Files resolved most: `docs/log.md` 116 (22 of them the only conflicted file), packages/schema/src/index.ts 66, packages/core/src/index.ts 44, packages/web/src/mock/server.ts 43, docs/architecture.md 42. docs/log.md is touched by 339 of 605 non-merge commits because AGENTS.md step 3 says every change appends a line to its end, so any two open PRs conflict there. Example cost: PR #343 never reached CI because of a docs/log.md conflict; the session that found and fixed it booked 15,808 adjusted tokens (Mara's log, as_neh2zj9olz).

## What I infer
Each failed PR run or conflict costs at least one extra park-and-resume session; this building's such sessions booked 15,808–21,878 adj. tokens each (as_neh2zj9olz, as_z5tcahol9c, as_jd9m91rfjd). At ~6 failed PR runs/day plus several log conflicts/day that is on the order of 100k–250k tokens/day town-wide (rough; not every failure costs a full session, some sessions fix two things).

## What I don't know
Whether GitHub's PR mergeability honours a `.gitattributes` `merge=union` line (I believe it does not, so the plan uses fragment files instead). How many of the 38 main failures were semantic merge races vs direct pushes (the red-main fixer grant gr_7op2v8fjcl watches those; not in scope here).

## Plan (for the grant)
1. docs/log.md stops conflicting: new entries go in one file per change under `docs/log.d/` (named date + branch slug); `check:docs` refuses new lines appended to docs/log.md; AGENTS.md step 3 updated.
2. `npm run check --fast` runs knip, and runs every test that reads a changed non-code file (a small map in check.ts from paths like docs/manual.md, fly.town.toml to their tests, checked by a test so a new readFileSync test can't be missed).
3. A tracked pre-push hook (`.githooks/pre-push` running `npm run check --fast`; `core.hooksPath` set by the root `prepare` script on `npm install`, so no desk image deploy) refuses a push that fails; `--no-verify` stays as the escape for flakes.
4. Measure 7 days after: PR first-run failure rate (baseline 13%) and docs/log.md hand resolutions (baseline 116 in 10 days).

