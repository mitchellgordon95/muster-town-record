---
id: "dc_69gfsko8l4"
type: "report"
state: "building"
title: "Agent teams step 3 merged (PR #148, 2f823fd): in a 1:1 Pix reads the code of main before answering"
authorId: "ag_nf93z7dbfe"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 3 merged (PR #148, 2f823fd), redeploy queued; your parked continuation runs the live check once 2f823fd is live. The end-to-end proof (a 1:1 where Pix cites file:line) needs Mitchell to ask; in the live check verify what a fork can (the copy at .tmp/code-main, the refs/muster-town/code-main fetch in the log, a manage session's tool list) and say plainly what still needs his 1:1. Rollup 34 Shipped candidate with the agent-teams item."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T02:17:27.363Z"
sessionId: "se_q2imd4azq8"
assignmentId: "as_h3sd56b4gz"
costUsd: 1.4761999000000001
tokens: 73810
turns: 35
createdAt: "2026-10-31T02:17:08.646Z"
updatedAt: "2026-10-31T02:17:27.363Z"
---
Once 2f823fd is live, Mitchell can ask Pix in a 1:1 "where is X handled?" and Pix reads the current code of main (Read, Grep, Glob; it can't edit or run anything) and answers with file:line.

## What I did
- The first attempt was never pushed, but its code was in a local stash, so I reused it. I then changed it to read main as it is on origin, not only the commit that was live when the server started.
- Merged PR https://github.com/mitchellgordon95/muster-town/pull/148 (merge commit 2f823fd) after merging in origin/main. The full `npm run check` passed (7m03s) and so did `--fast` after the merge. Queued a redeploy (started).

## Findings
- **What changed** (`packages/runtime/src/code.ts`):
  - The runtime fetches origin's `main` into a private ref, `refs/muster-town/code-main`. It does this at start, then from the tick at most every 5 min, and never while the redeploy lock file exists. The fetch leaves origin/* and HEAD alone, so the redeploy pull is not disturbed.
  - When that ref moves, the runtime `git archive`s it into `.tmp/code-main`, which is gitignored. The new copy is swapped in whole, so a session never sees a half-written tree.
  - If there is no origin, the copy is the live HEAD.
- **What a manage session gets** (in-tray or 1:1):
  - `cwd` is the copy, and the only built-in tools are Read, Grep and Glob.
  - A PreToolUse hook blocks any path outside the copy (it follows symlinks) and every other built-in tool (Bash, Write, Edit, Task, Agent…).
  - A "## The town's code" prompt block tells Pix to read the code and cite file:line, and that main may be ahead of what is live.
  - The session never waits on a fetch: it uses the copy as it is when it starts.
- **Tests:** `packages/runtime/test/code.test.ts` has 4 tests:
  - fetching follows main, with the 5-min throttle and the redeploy lock;
  - the guard, including a symlink escape and every write/run tool;
  - `townOptions` tools and cwd;
  - a runtime run where the manager's session gets the tools and the prompt block.
- **Not yet verified live.** The check for the next session: open a 1:1 with Pix and ask "where is stop_fork's hard stop handled?". The transcript should show a Grep or Read, and the answer should cite `packages/core/src/forks.ts`. Docs updated: architecture.md (Manager session) and log.md. Topic page: [dc_qhgxudus5c](../../wiki/2026-10/2026-10-31-agent-teams-forks-vs-claude-code-agent-teams-gxudus5c.md).

## What I need from you
Nothing needed. I'll run the live check once 2f823fd is live.
