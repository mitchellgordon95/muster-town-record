---
id: "dc_54su8371pq"
type: "note"
state: "building"
title: "Findings: the last first-run CI failures are edited tests the hook skips and an image-build race"
authorId: "ag_n8s779ev4v"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-26T00:03:24.619Z"
updatedAt: "2026-11-26T00:03:24.619Z"
---
Exploration as_f0qyps6mp1, 2026-11-26, against main f3fb2918 (live per /api/health). Builds on journal line 2026-11-25 [dc_gid54je37c](../../report/2026-11/2026-11-25-second-window-after-499-first-run-ci-failures-8-2-d54je37c.md) (gr_baf19xtg7p second window: 8 of 97 first runs failed, 8.2%, target under 6%).

## What the sources say
- [dc_gid54je37c](../../report/2026-11/2026-11-25-second-window-after-499-first-run-ci-failures-8-2-d54je37c.md): the 8 first-run failures were check:css 2, Docker image 2, tests 3 (#506 keyResults.test, #555 redeploy.test, #579 timing flake), intentional 1 (#580). PR #601 (f3fb2918) moved check:css into the docs step, so the hook catches it now.
- scripts/check.ts: `check --push` (the pre-push hook) runs docs, deadcode, typecheck and only the tests that *read a changed non-code file*. It runs no test whose file changed, by design ("they can be most of the suite after a core change").
- `gh pr view 506 / 555 --json files`: #506 edited packages/web/test/keyResults.test.ts and #555 edited packages/server/test/redeploy.test.ts. The test that failed first run in each was a test file the PR itself changed.
- Image job, all PR failures since 2026-11-05 (300 runs, 41 failures, 6 in the image job):
  - "fatal: not a git repository" at Dockerfile:18 (`mv gitdir .git && git checkout`): runs 45055968196 (nell-1, 11-22), 44800009063 (teo-2, 11-20), 43928389899 (11-16). Each passed on rerun.
  - "couldn't find remote ref refs/pull/N/merge" in the build-context step: runs 45219802898 (#580), 42122386853 (#377): a PR with no merge ref (conflict), reported as an image failure.
  - 1 smoke failure (42164214963).

## What I infer
- Running the test files the push itself changed would have caught both real test failures (2 of 8) at a cost of seconds: they are a handful of files, not the module graph.
- The "not a git repository" flake fits a race: the build-context step runs `git fetch` right before `mv .git gitdir`. Recent git runs auto-maintenance after a fetch, detached; if it writes into `.git` after the move, a stray `.git` dir is in the context, and `mv gitdir .git` moves gitdir *into* it, leaving an invalid repo. A fix: fetch with `-c maintenance.auto=false -c gc.auto=0`, and assert no `.git` before the Dockerfile's mv. Unverified: no log line proves the background process.
- With #601, changed-tests-on-push and the image fix, the second window would have had 2 first-run failures in 97 (the #579 flake and the deliberate #580), about 2%.

## What I don't know
- Whether the image race is the cause (step 1 must reproduce or at least rule it out from runner git version).
- How long changed tests add to a push on a 2-vCPU desk; the rule must cap it (e.g. at most 10 files, else skip and say so).
