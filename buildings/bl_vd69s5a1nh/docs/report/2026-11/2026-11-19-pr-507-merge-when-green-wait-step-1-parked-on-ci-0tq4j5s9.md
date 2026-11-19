---
id: "dc_w10tq4j5s9"
type: "report"
state: "building"
title: "PR #507: merge-when-green wait (step 1); parked on CI"
authorId: "ag_gvmeqnaxx9"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T15:30:40.568Z"
sessionId: "se_7k0mc9suxv"
assignmentId: "as_y6plwts4cr"
costUsd: 2.2323052999999993
tokens: 111615
turns: 38
createdAt: "2026-11-19T15:30:40.561Z"
updatedAt: "2026-11-19T15:30:40.568Z"
---
## What I did
I built step 1 of gr_rlt0ctnhqk and opened draft PR #507 (https://github.com/mitchellgordon95/muster-town/pull/507). `npm run check --fast` passes on my desk: docs, deadcode, typecheck and 313+ tests, 7m26s in total. I am parked on the PR's CI.

## Findings
- **Schema.** The `{pr: N}` wait takes an optional `merge: true`.
- **Runtime (packages/runtime/src/pr-checks.ts, `mergeGreen`).** It acts when every check has passed and GitHub says `mergeable` is true. It marks a draft ready through GraphQL, squash-merges with "<title> (#N)" pinned to the head sha, and deletes the branch. It caches the PR as `merged` with `mergeSha` and `mergedBy: town`.
- **When the wait wakes the session instead.** A conflict, red checks, a branch that is not `agent/…` (or comes from a fork repo), no token, or a GitHub refusal such as a required review.
- **When it tries again on the next poll.** When `mergeable` is null, on a 409 (the head moved), or on a 405 "Base branch was modified".
- **Core (waits.ts `closeMerged`).** The parked continuation closes as done with no session. Its job's thread gets an entry "merged PR #N as <sha8>", and a `pr.merged` event fires. A parked grant step queues its next step. Every woken `{pr}` continuation now has the PR's outcome added to its description, e.g. "PR #179 when this resumed: failed (check)".
- **Tests.**
  - pr-checks.test.ts has 6 new cases: merge, red, conflict or null, refused or retried, non-agent branch, and a plain wait that is unchanged.
  - grant-steps.test.ts has 2 new cases: a merged step queues step 2 and has no session; a failed merge wakes with the reason.
  - docs/wakes.md and a docs/log.d entry describe the change. The topic page "Merge when green" ([dc_f57lvgd1du](../../wiki/2026-11/2026-11-19-merge-when-green-7lvgd1du.md)) holds the design.
- **Not checked yet.** We don't know whether the town's repo token is allowed to merge and mark a PR ready. That is the stop condition, and the first live trial will show it.

## What I need from you
Nothing needed.
