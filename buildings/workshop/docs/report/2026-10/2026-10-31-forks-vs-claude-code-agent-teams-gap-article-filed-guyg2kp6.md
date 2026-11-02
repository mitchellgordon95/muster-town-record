---
id: "dc_n3guyg2kp6"
type: "report"
state: "building"
title: "Forks vs Claude Code agent teams: gap article filed (dc_i7ji4xacd9), 5 gaps, 4-step build order"
authorId: "ag_pf0szp7x4j"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_i7ji4xacd9","dc_zqw46y3zm8","mt_ufwllf4wmt"],"urls":["https://code.claude.com/docs/en/agent-teams"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Article dc_i7ji4xacd9 filed with 5 gaps and a 4-step build order; no background tasks this time, 38k tokens. The four steps go on the queue as directed work (1:1 mt_ufwllf4wmt decision 2)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T01:29:40.165Z"
sessionId: "se_ovuk9eoehl"
assignmentId: "as_zoyv05vcyl"
costUsd: 0.7703978
tokens: 38520
turns: 17
createdAt: "2026-10-31T01:28:17.229Z"
updatedAt: "2026-10-31T01:29:40.165Z"
---
## What I did
I read the source card [dc_zqw46y3zm8](../../../../../library/source/2026-10/2026-10-31-source-claude-code-docs-orchestrate-teams-of-claud-w46y3zm8.md). It already had all six facts, so I didn't fetch the doc again or change the card. I read the fork, interrupt, tell, desk-control, manage-session and teamBlock code on main at 1ef98cc, in the foreground, without subagents. Then I filed the article [Forks vs Claude Code agent teams: the gaps](../../article/2026-10/2026-10-31-forks-vs-claude-code-agent-teams-the-gaps-ji4xacd9.md) in the Workshop filing cabinet. No code changes.

## Findings
- **Article [dc_i7ji4xacd9](../../article/2026-10/2026-10-31-forks-vs-claude-code-agent-teams-the-gaps-ji4xacd9.md):** it has 10 table rows with file:line for each, and **5 gaps**:
  1. A manager can't reach a running fork mid-session. Agent `tell`s only land in the fork's inbox (social.ts:84).
  2. There is no interrupt the manager agent can use. The interrupt pipe (ops.ts:508, desk.ts:54) is for humans only.
  3. The manager can't stop a fork, and no stop lets the fork wrap up and file its report.
  4. The manager can't see a running fork's progress. Its manage and 1:1 session has no code tools (session.ts:57, 222-234) and no town tool for a fork's transcript.
  5. There's no plan-approval step.
- Already close to agent teams: lead and teammates, the shared task list (the building queue with `waitFor`), and finish notifications (in-tray plus `wakeManager`).
- Small inconsistency: the manager's prompt says "forks don't take messages" (memory.ts:307), but humans can message a live fork mid-session (ops.ts:366-399).
- **Build order:**
  1. A manager's `tell` to a live fork is also delivered as an interrupt mid-session, and the prompt line is fixed.
  2. A `fork_status` town tool for the manager: the fork's assignment, tokens so far, and its last tool calls from the live transcript. Mitchell asks in a 1:1 "what is Pix 4 doing?" and gets a real answer.
  3. In a 1:1, the manager's session can read a read-only checkout of main (Read/Grep/Glob only).
  4. `stop_fork`: asks the fork to file its report and stop, then stops it hard after a timeout.
- **Not known:** whether the web Fork tab already has a message box for a live fork; whether a report filed during a live manage session reaches that session; how often a desk checks for interrupts.

## What I need from you
Nothing needed.
