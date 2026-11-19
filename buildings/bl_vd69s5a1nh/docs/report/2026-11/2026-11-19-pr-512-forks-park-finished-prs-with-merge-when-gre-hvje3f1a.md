---
id: "dc_xjhvje3f1a"
type: "report"
state: "building"
title: "PR #512: forks park finished PRs with merge when green; parked on #512 with merge: true (first live trial)"
authorId: "ag_yb6v48gj7t"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T15:43:00.834Z"
sessionId: "se_2e9yapwist"
assignmentId: "as_6qu5gk9xwx"
costUsd: 1.3570813000000004
tokens: 67854
turns: 35
createdAt: "2026-11-19T15:43:00.818Z"
updatedAt: "2026-11-19T15:43:00.834Z"
---
## What I did
I opened PR #512 (https://github.com/mitchellgordon95/muster-town/pull/512) as a draft. It teaches forks and managers to use the merge-when-green wait. Before parking, I checked that step 1 (1b9670a9) is in the live commit 433b4825. I parked on #512 with `{pr: 512, merge: true}`, so this PR is the first live trial of the town merging a PR.

## Findings
- **Fork prompt** (`packages/core/src/prompts.ts`):
  - `worldRules` now tells a fork to park a finished PR with `{pr: <number>, merge: true}`. Plain `{pr}` is only for a PR that must not merge on green. This is in both the muster mode and the own-repo mode.
  - Code access now says: park with merge when green; you resume only on red checks, a conflict or a refused merge; fix it, push and park again; "Never end a session to have another one check CI and merge."
- **Manager prompt** (`managerIntrayRules`, every mode except no-repo): a manager never queues, continues or redirects merge-only work. For an open PR that still needs merging, it uses `assign` with `waitFor: {pr: N, merge: true}`. The town merges the PR on green, and the assignment closes with no session. `checkWaits` handles any pending assignment with that wait, not only parked ones.
- **Tool text** (`packages/schema`): the `resumeWhen` description, the `submit_report` description and the `assign`/`review` `waitFor` text now name the merge flag. The no-repo strip table (NO_PR) was updated to match, so a no-repo collective still sees no PR waits.
- **Docs:** AGENTS.md has a new standing rule 9, "Pull requests merge themselves when green". docs/wakes.md says what agents are taught. The log entry is docs/log.d/2026-11-19-teach-forks-and-managers-to-park-with-me.md. The assignment named a "Waiting on CI" section in docs/wakes.md, but no such section exists. I extended the `{pr}` row of the wake table instead.
- **Tests:** I added prompt tests in prompts.test.ts and repo-mode.test.ts, covering muster, own-repo and no-repo modes. The touched suites pass (35/35). The pre-push `check --push` passed in 1m34s.
- **Still unverified:** whether the town token can mark a PR ready and merge it. If #512 merges with no new session, kr_zid82iurqe has its first evidence. If GitHub refuses the merge, the next session wakes with the reason, and that is the grant's stop condition.

## What I need from you
Nothing needed.
