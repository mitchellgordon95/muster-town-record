---
id: "dc_ub7y4fh1he"
type: "report"
state: "building"
title: "Forks park on CI with {pr: N}: merged as 43a7f6f (PR #190), redeploy requested; parked for the live check"
authorId: "ag_8obi1lzxpo"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. {pr: N} wait merged as 43a7f6f (PR #190). The live check (blocked text, unblock event, line on dc_hai9ky5u7a) runs as the parked continuation as_je1inot6lq, waiting on deploy 43a7f6f. Thanks for the stash note: nothing committed from it."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T20:51:58.935Z"
sessionId: "se_f5a535pewd"
assignmentId: "as_7a33e2woff"
costUsd: 3.0742108000000012
tokens: 153711
turns: 70
createdAt: "2026-10-31T20:50:11.218Z"
updatedAt: "2026-10-31T20:51:58.935Z"
---
## What I did
Built a new wait kind `{pr: N}` so a fork waiting on CI parks on the PR itself instead of guessing an `{after}` time (Mitchell, 1:1 mt_3jtclcoxl2). PR https://github.com/mitchellgordon95/muster-town/pull/190. CI went green in 1m37s, I merged it as **43a7f6f** and requested a redeploy. At report time the live commit was 08a9831, which does not include 43a7f6f yet. I parked this work until that deploy.

## Findings
- **How the wait works:** `{pr: N}` holds until every check on the PR's head commit has finished, passed or failed. It also releases if the PR is merged or closed. It works in `submit_report resumeWhen` and in `assign`/review `waitFor`. `{after}` stays, for real times only.
- **How the server watches GitHub:** the new file `packages/runtime/src/pr-checks.ts` runs about once a minute, from the scheduler tick. It only reads PRs that a pending wait names. For each one it reads the PR, its check suites and its check runs, using the repo token the redeploy already uses.
  - Some apps installed on the repo (render, vercel, claude, railway) create check suites with no runs, and those stay "queued" forever. The poller ignores them.
  - It waits for the whole workflow to finish, not only the jobs it has seen so far.
  - Once a commit's checks have finished, the result is cached for good.
  - `waitMet` reads the cache through `world.host.prChecks`. Without a running server the wait never releases and expires after 24 h, the same as `{deploy}`.
- **What you'd see:** in an agent's queue and the red map badge's hover card, "waiting on PR #190 checks: 3 min so far (1 of 2 done)". When the wait releases, the event log says "… unblocked: PR #190's checks to finish (failed: check) happened" (or "passed").
- **Where the text tells agents about it:**
  - The `submit_report` and `assign` tool descriptions and the desk brief's parking line say: use `{pr: N}`, never an `{after}` guess for CI.
  - The workshop prompt now says to park on the PR after `gh pr create`.
  - Docs updated: docs/wakes.md, docs/architecture.md and the invariants doc.
  - `scripts/town-blockers.py` now has a `pr` row, so time held on CI counts as a real blocker.
- **Tests:**
  - A new case in core `waits.test.ts` fails on main (1 failed of 10) and passes with the change. I checked this by reverse-applying the source diff.
  - A new runtime `pr-checks.test.ts` runs against a fake GitHub: pending, waiting for the whole workflow, passed, failed, merged, the once-a-minute throttle, and no calls when nothing waits.
  - Full suites: core 532/532, runtime 190/190, web 189/189. `npm run typecheck` and `check:docs` pass.
  - Against the real GitHub API, PRs #182 and #179 both read as passed (2 of 2 checks).
- **Topic pages:**
  - "Live checks and dev habits" ([dc_cvnjh0v7mj](../../wiki/2026-10/2026-10-28-live-checks-and-dev-habits-njh0v7mj.md)): the CI line now says park on `{pr: N}`. Until 43a7f6f is live, it says to watch CI with `gh pr checks N --watch` in the foreground instead.
  - "Wakes and blocked-assignment reasons" ([dc_mhz91klzjk](../../wiki/2026-10/2026-10-28-wakes-and-blocked-assignment-reasons-z91klzjk.md)): new line on `{pr}` waits.
  - "Rollup 35 materials" ([dc_hai9ky5u7a](../../wiki/2026-10/2026-10-31-rollup-35-materials-i9ky5u7a.md)): Shipped candidate with What it is / What you'd see / Your call: None.
- **Slip:** a `git stash pop` briefly applied the old unrelated auto-stash (stash@{0}) to my checkout. I reverted those files to HEAD, nothing was committed from it, and the stash entry is still there.
- **Plan for the continuation:**
  1. Confirm with `/api/health` that 43a7f6f is live.
  2. Find a real `{pr}` park, or create one with an assign `waitFor {pr: 190}`. #190 is merged, so it should release within about 60 s.
  3. Read `GET /api/blocked` for the blocked text and look in the event log for the "unblocked: PR #… checks" line.
  4. Record the result on [dc_hai9ky5u7a](../../wiki/2026-10/2026-10-31-rollup-35-materials-i9ky5u7a.md).

## What I need from you
Nothing needed.
