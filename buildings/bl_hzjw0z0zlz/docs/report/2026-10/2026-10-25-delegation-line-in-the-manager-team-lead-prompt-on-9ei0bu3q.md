---
id: "dc_vi9ei0bu3q"
type: "report"
state: "building"
title: "Delegation line in the manager team-lead prompt on main (PR #49, 9aa87fa): decisions and rollups only, every task becomes an assignment, independent tasks to different residents in parallel"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":["https://github.com/mitchellgordon95/agent-town/pull/49"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": The @-mention reply path is observed: Mitchell mentioned Kelly in this town hall and she answered from a meeting-reply session. Kelly confirms the literal sessi"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-25T14:34:19.631Z"
sessionId: "se_rfshcs3gzy"
assignmentId: "as_6wr9fg5bkh"
costUsd: 1.0038261
tokens: 25625
turns: 22
createdAt: "2026-10-25T00:07:57.662Z"
updatedAt: "2026-10-25T14:34:19.631Z"
---
## What I did
Added one rule to `managePrompt` in packages/core/src/prompts.ts, the user prompt of the manager's team-lead session (waterfall step 2). It now says: a manager does only decisions and rollups; any task that appears (verifying, writing, fixing, checking something live) becomes an assignment the moment it appears, never the manager's own next session; independent tasks go to different residents in parallel, one `assign` each, not queued on one resident. Prompt only, no board rule, as Mitchell decided.

Added a core test that asserts the four phrases are in the prompt, noted the rule in docs/waterfall.md §3.1 and docs/log.md. Typecheck clean; core prompts tests 8/8 and runtime manage tests 4/4 green.

PR: https://github.com/mitchellgordon95/agent-town/pull/49, merged to main as 9aa87fa under the push-to-main rule. Redeploy queued (restarts after this session ends); 9aa87fa should be live after it.

## Findings
- No test covered the team-lead prompt's text before this; the new one does.
- The rule takes effect in every managed building's next team-lead session (the prompt is built per session), nothing to migrate.
- The in-tray block and work sessions are unchanged: the rule lives only in the team-lead session, where the manager has no code or web tools anyway.

## What I need from you
Nothing needed. Verify next session that `https://muster.town/api/health` reports a commit containing 9aa87fa.
