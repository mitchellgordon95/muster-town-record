---
id: "dc_iga04ts2ru"
type: "report"
state: "building"
title: "fork_status shipped (PR #142, 3e6c790): in a 1:1, \"what is Pix 4 doing?\" now gets a real answer"
authorId: "ag_7h5bd7n3ib"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: agent-teams step 2, fork_status (PR #142 = 3e6c790), a manager or reviewer sees a live fork's assignment, runtime, booked tokens and last tool calls; only Bank code is a read of adjustedOutputTokens; no migration. Live check queued separately (waits deploy 3e6c790)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T01:59:39.039Z"
sessionId: "se_rt8qy08v3v"
assignmentId: "as_52s63s7wiu"
costUsd: 2.3934377000000002
tokens: 119672
turns: 61
createdAt: "2026-10-31T01:59:18.236Z"
updatedAt: "2026-10-31T01:59:39.039Z"
---
In a 1:1 Mitchell can now ask Pix "what is Pix 4 doing?". Pix calls `fork_status` and answers with the fork's assignment, how long it has run, the tokens booked so far, and its last 10 tool calls, each with the first line of its input and of its result.

## What I did
- Built step 2 of [dc_i7ji4xacd9](../../article/2026-10/2026-10-31-forks-vs-claude-code-agent-teams-the-gaps-ji4xacd9.md): a town verb `fork_status {forkId | assignmentId, limit=10}` for the manager and reviewers (building.assign on the fork's building, or anyone allowed to read its transcript). Manage sessions get every town verb, so it works in their 1:1s too, and teamBlock's "Live forks" line now mentions it.
- PR https://github.com/mitchellgordon95/muster-town/pull/142, merged as **3e6c790** after three merges of main (steps 1 and 4 landed while I worked; I resolved the conflicts in memory.ts, verbs/index.ts and describe.ts). Queued a redeploy with `image: true` because the desk code changed. **3e6c790 should be live**; I have not checked it.
- Full `npm run check` (docs, deadcode, typecheck, tests) passed on the merged branch: 515 + 181 + 225 + 25 + 37 + 165 tests. A typecheck also passed after the last clean merge.

## Findings
- **Where the data comes from.** A kept transcript exists only after a session ends (docs/transcripts.md), so a live fork's tool calls are read from its session's `agent.tool` events, which now carry `toolUseId`. Results come from `world.toolResults`, a new in-memory ring (100 per session, 200 sessions). Host sessions fill it from tool_result blocks. Desks post a new activity kind `result` (`toolUseId`, first line, `isError`). Tokens are `sessionView(session).adjustedOutputTokens`, i.e. what the Bank has booked so far. The only Bank code involved is that read, and there is no migration.
- **Limits.** Results are not stored, so after a server restart a call shows `result: null`, and desks still running an image older than 3e6c790 also show `result: null`. The tool calls themselves come from the event log, so they survive a restart.
- **Test.** The runtime test `packages/runtime/test/fork-status.test.ts` covers:
  - a fork's live session with Bash, Read (error) and Grep calls, where the Grep result arrives through the desk path `onDeskActivity` kind `result`
  - the manager sees the assignment, the lane, tokens > 0, input/result lines and the latest thought
  - the `assignmentId` lookup with `limit: 1`
  - a non-manager (Noor) is refused
  - after retirement it reports the session done with its report id
  - `TOWN_TOOLS` contains `mcp__town__fork_status`
- Topic page [dc_nrrzs44q4z](../../wiki/2026-10/2026-10-28-session-transcripts-and-who-can-read-agent-memory-rzs44q4z.md) rewritten with the live-view section.
- Still to do: a live check. In a 1:1 while a fork is running, ask "what is Pix N doing?" and the answer should quote its recent calls. The full answer with results needs a desk recreated on the new image.

## What I need from you
Nothing needed.
