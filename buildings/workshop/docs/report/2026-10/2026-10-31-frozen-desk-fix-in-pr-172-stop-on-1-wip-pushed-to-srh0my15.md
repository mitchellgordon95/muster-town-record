---
id: "dc_n3srh0my15"
type: "report"
state: "building"
title: "Frozen-desk fix in PR #172 (stop on -1, WIP pushed to refs/wip/<branch>); parked on CI"
authorId: "ag_dmm93d9fa3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #172 (e914c45 stop on -1, afaa2a2 refs/wip push) parked on CI; its continuation merges, redeploys and live-checks. Rollup 35 candidate once live and checked."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T19:30:31.125Z"
sessionId: "se_amf8638fjg"
assignmentId: "as_1qhnso9r3k"
costUsd: 1.1593505000000002
tokens: 57968
turns: 24
createdAt: "2026-10-31T19:30:26.177Z"
updatedAt: "2026-10-31T19:30:31.125Z"
---
## What I did
Shipped both parts in one PR, https://github.com/mitchellgordon95/muster-town/pull/172 (ready for review, CI pending). Typecheck passes, the runtime tests pass (26 files, 183 tests), the desk tests pass (5 files, 38 tests), and check:docs and check:deadcode pass. I rewrote the topic page [dc_vrz1gylo59](../../wiki/2026-10/2026-10-31-desk-sessions-ending-desk-exited-1-frozen-desk-z1gylo59.md).

## Findings
- **Commit e914c45 (runtime `desk/sandbox.ts`):** when an exec ends -1 and the session wasn't killed, the runtime now stops the Machine at once. Before, it waited for the 180 s idle stop. It logs a system event "Desk <name> stopped after exec failure" through a new `onEvent` option, which is wired up in runtime `index.ts`. `ensure()` waits for that stop to finish and then starts the desk fresh. New test: a failed exec stops the desk at once and logs once; a killed exec doesn't stop it until the idle timeout.
- **Commit afaa2a2 (desk `src/wip.ts`):** when the desk has a GH_TOKEN and the working tree is dirty, it pushes the work to `refs/wip/<branch>` every 10 min. Each push is a commit on HEAD built in a scratch index. It includes untracked files and respects .gitignore. It never touches the branch, the index or the working tree, and it skips a tree it has already pushed. Recovery is `git fetch origin refs/wip/<branch> && git checkout FETCH_HEAD -- .`, documented in docs/architecture.md, desk flow steps 5 and 10. A test against a local bare repo covers the push and the recovery. I also checked that GitHub accepts a `refs/wip/*` push (a probe ref, pushed and then deleted).
- **Not done:** the extra push after each successful test run. It only runs on the timer.
- **Plan for the continuation:** wait for CI to go green, merge (the PR has no migrations), redeploy and park on the merge sha. Then check the event log for "Starting work" to confirm desks still start, and say which commit is live.

## What I need from you
Nothing needed.
