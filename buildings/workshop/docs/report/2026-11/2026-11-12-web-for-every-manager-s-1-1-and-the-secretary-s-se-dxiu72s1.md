---
id: "dc_2jdxiu72s1"
type: "report"
state: "building"
title: "Web for every manager's 1:1 and the Secretary's sessions: PR #426 open, parked on CI"
authorId: "ag_xj16viedyy"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Scope matches decision 2 of mt_msnjkpgwdb (web for the Secretary everywhere and every manager's 1:1; team-lead sessions of other managers unchanged). The continuation as_6kosemv1p6 is already waiting on PR #426's CI: merge when green, park on the merge sha, then check live via the Secretary's next 1:1 tool events. Folded into the next rollup once it is live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-12T14:56:57.133Z"
sessionId: "se_8t1bx5jrqw"
assignmentId: "as_i5eq80n2zu"
costUsd: 0.7287882
tokens: 36439
turns: 15
createdAt: "2026-11-12T14:56:47.618Z"
updatedAt: "2026-11-12T14:56:57.133Z"
---
## What I did
Read session.ts / manage.ts / meetings.ts / work.ts, added `webFor` and wired it into every in-process session kind. PR https://github.com/mitchellgordon95/muster-town/pull/426 (commit 50d77a76), CI running; parked on it.

## Findings
- **Change:** `webFor(purpose, {secretary, oneOnOne})` in packages/runtime/src/session.ts decides web (WebSearch, WebFetch). Work: always (unchanged). Manage: on in **every manager's 1:1**, and in **all of the Secretary's** manage sessions (team-lead included). Meeting @-replies: the Secretary only. Facilitation: never. Tool lists otherwise unchanged: no Bash/Write/Edit in-process; code stays read-only (Read/Grep/Glob) where it was.
- **Why every manager's 1:1 and not every team-lead session:** a 1:1 with a human is the same kind of session for every manager, and the human's question may need a pricing page or a doc. Other managers' team-lead sessions decide reports from town docs; leaving them unchanged keeps their tool list (part of the cached prefix) and their context free of large fetched pages. The Secretary gets it everywhere because Mitchell asked for it.
- **Edge:** a 1:1 that cuts into an already-running team-lead session (non-Secretary) keeps that session's tools, so no web there until a fresh session starts. Noted in docs/architecture.md.
- **Tests:** new packages/runtime/test/session-tools.test.ts (the webFor table; townOptions with web on gives WebSearch/WebFetch and still disallows Bash/Write/Edit/Read/Task/Agent). one-on-one.test.ts now asserts a 1:1 session's tools = [WebSearch, WebFetch]; manage.test.ts still pins a team-lead session to []. Local: 4 files, 25 tests pass; typecheck passes.
- Docs: architecture.md and meetings.md tool lines updated. Log: docs/log.d/2026-11-12-pix-2-secretary-web.md. Only runtime and docs changed; no other building's files.
- **Next session:** merge when green, park on {deploy: merge sha}, then check live: tell the Secretary (ag_7tiwyqva83) to use WebFetch in its next 1:1, or read that session's tool events.

## What I need from you
Nothing needed.
