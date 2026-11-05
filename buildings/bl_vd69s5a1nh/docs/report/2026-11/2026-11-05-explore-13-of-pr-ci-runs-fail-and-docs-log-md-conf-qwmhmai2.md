---
id: "dc_vfqwmhmai2"
type: "report"
state: "building"
title: "Explore: 13% of PR CI runs fail and docs/log.md conflicts 116 times in 10 days; proposed gr_baf19xtg7p (300k) to catch these before push"
authorId: "ag_lrhozhxrq3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_z9oix2r66w","dc_wp3isidhw8"],"urls":["https://github.com/mitchellgordon95/agent-town/actions/workflows/ci.yml"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Good exploration: the numbers (13% PR CI failures, docs/log.md in 116 of 195 hand-resolved merges) are concrete and the proposal gr_baf19xtg7p is in the Town Hall in-tray where Mitchell decides it. Nothing to assign until he does; the work is parked on the proposal."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-05T00:07:45.765Z"
sessionId: "se_8quixzrc3w"
assignmentId: "as_7pj1s11lp3"
costUsd: 1.2882127
tokens: 64411
turns: 32
createdAt: "2026-11-05T00:07:32.708Z"
updatedAt: "2026-11-05T00:07:45.765Z"
---
## What I did
I picked one direction: PR round-trips. These are the extra park-and-resume sessions an agent spends when its PR fails CI or conflicts with main. I pulled 10 days of ci.yml runs (2026-10-25 → 11-04) and sorted the 97 failed runs by the first thing that failed in their logs. I also counted hand-resolved files in the "merge main into branch" commits on origin/main. The findings are in [dc_z9oix2r66w](../../note/2026-11/2026-11-05-findings-where-pr-round-trips-are-wasted-ci-failur-oix2r66w.md) and the topic page [dc_wp3isidhw8](../../wiki/2026-11/2026-11-05-pr-round-trips-ci-failures-and-merge-conflicts-3isidhw8.md). I filed one proposal, gr_baf19xtg7p. No code changed.

## Findings
- **PR CI:** 59 of 442 runs failed (13%). On pushes to main, 38 of 495 failed.
- **Causes of the 97 failed runs:**
  - knip dead code: 24
  - check:docs: 13
  - typecheck: 10
  - 1–3 failing tests: 38
  - a real break with many failing tests: 9
  - promote job curl 503: 3
- **Most-failed tests:** web `manual.test.ts` failed 11 times and core `finance-fly.test.ts` 8 times.
- **Why the local check misses these:** `npm run check --fast` skips knip, and `vitest --changed` never re-runs those two tests because they read docs/manual.md and fly.town.toml with readFileSync. No pre-push hook is installed on desks.
- **Conflicts:** 195 of the 229 "merge main into branch" commits had hand resolutions. docs/log.md was in 116 of them, and in 22 it was the only conflicted file. The next most-conflicted file is schema/index.ts at 66. The cause is AGENTS.md step 3: every PR appends a line to the end of docs/log.md, so any two open PRs conflict there. Example: PR #343 never reached CI because of this conflict, and the session that fixed it cost 15,808 tokens.
- **Rough cost:** extra sessions here cost 15,808–21,878 adjusted tokens each. Town-wide, I estimate 100k–250k tokens a day; that figure is uncertain.
- **Proposal gr_baf19xtg7p (300,000 tokens):**
  - Log entries move to one file per change under docs/log.d/, and check:docs refuses new lines in docs/log.md.
  - `--fast` runs knip, plus any test that reads a changed docs or config file.
  - A tracked pre-push hook runs the fast check. npm install sets it up, so desks get it without an image deploy.
  - A 7-day observation then checks the PR failure rate against the 13% baseline (target under 6%).
- Not in scope: test flakes (stale-state drain, export timer).

## What I need from you
Decide whether to fund gr_baf19xtg7p. It changes AGENTS.md and the root scripts, which every building uses, so the docs/log.md change affects everyone.
