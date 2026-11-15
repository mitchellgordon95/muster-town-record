---
id: "dc_yh19s7fa22"
type: "report"
state: "building"
title: "Goal proposals on the thread (decision 4): PR #465 open, parked on CI"
authorId: "ag_kxn9u5q1fk"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. PR #465 (goal proposals on the thread, decision 4 of mt_dwsxo7oms8) is open as a draft and the merge continuation as_k7zilvsvbw waits on its CI; nothing else to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-15T22:45:10.510Z"
sessionId: "se_6g7hf5wh1z"
assignmentId: "as_mccm7h9y3r"
costUsd: 0.6153952
tokens: 30770
turns: 15
createdAt: "2026-11-15T22:44:54.109Z"
updatedAt: "2026-11-15T22:45:10.510Z"
---
## What I did
I recovered the uncommitted work from Pix 2's dead session as_3f4qsq15tt. It was desk stash@{0}, on top of main 45703173, and applied cleanly. Nothing had been pushed and there was no PR. I renamed the log.d file for my branch. I ran typecheck and the core tests below one file at a time, then the full `npm run check -- --fast`, which passed (docs, deadcode, typecheck, tests; 9m04s). I committed, pushed, and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/465. Branch: agent/pix-1/goal-proposals-join-the-thread-model-mit.

## Findings
- `propose_goal` writes the proposal entry `en_<gp>` on the proposing building's thread (jb_town-hall for a human or the Planner). The town then files the need `en_<gp>_need`: kind goal, targetKind goalProposal, policy, Accept / Edit and accept / Cut (needs.ts `fileGoalProposal`). The manager writes the card, and the door keys on the need as in PR #463.
- `decideProposal` edits the tree and retires the ask, which answers the need. `decideAsk` on a goal-proposal ask is refused and points to the proposal decide route. A superseded proposal retires its asks. The inbox spam to editors (`notifyEditors`) is removed.
- The raw goal-proposal row has left the decision queue, the review deck and the intray routes (web and core). It has no fallback rendering.
- Migration: `backfillAsks` at boot gives every open proposal its entry and need. This covers gp_8lh67t75wj and gp_qxy3evg5dn.
- Tests passing: goal-proposal-thread (6, new), goals (14), goals-step4 (6), goals-step5 (7), needs (6), asks (10), review-deck (10), ask-entry-point (2), and web 308/308. Invariant: asks.md 21. Topic page: [dc_1h70f3fmo3](../../wiki/2026-11/2026-11-15-goal-proposals-on-the-thread-mt-dwsxo7oms8-decisio-70f3fmo3.md).

## What I need from you
Nothing needed. The session resumes on PR #465's CI to merge it.
