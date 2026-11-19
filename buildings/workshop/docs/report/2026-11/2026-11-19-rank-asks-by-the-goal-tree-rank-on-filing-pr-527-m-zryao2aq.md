---
id: "dc_rfzryao2aq"
type: "report"
state: "building"
title: "Rank asks by the goal tree, rank on filing: PR #527, merges when green"
authorId: "ag_8bhimuq5gg"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T19:16:48.106Z"
sessionId: "se_wg66pyi2to"
assignmentId: "as_rr6ry226co"
costUsd: 1.6378241
tokens: 81891
turns: 28
createdAt: "2026-11-19T19:16:48.081Z"
updatedAt: "2026-11-19T19:16:48.106Z"
---
## What I did
Mitchell asked for this in 1:1 mt_mjxwzdhhd7. I changed the Secretary's ranking in town code, so every collective gets it, and opened PR #527 (https://github.com/mitchellgordon95/muster-town/pull/527). It merges when its checks pass.

## Findings
**(a) The ranking rule is the goal tree, not a ledger line.** A new constant `RANK_RULE` in packages/core/src/secretary.ts is used in three places: RANK_RUN_PROMPT step 2 (the daily run), DECISION_RUN_PROMPT step 4 (the re-rank after a decision), and the 1:1 brief. Its text:

> "this collective's own goal tree (the read opens with its root goal; each ask shows its goal path and depth, 0 = the root): first, how directly the ask moves the root goal; second, how much it moves the rest of the tree; third, how much funded work it holds (work parked on it, money a building waits on, a click that unblocks another ask); last, age (older first). The do asks go last (a do asks a human to leave the queue and act in the world). A new ask arrives with a default rank from code (below every ask whose goal is as near the root or nearer): judge it by the whole rule."

Step 2 now reads: "Order every open ask, most urgent first, by RANK_RULE. The humans' past fund and reject decisions, with their notes, show how they weigh within that order: follow them."

The rank read (`rankInputsText`) now:
- opens with "The root goal of this collective (rank by how directly each ask moves it, then the rest of the tree): <root text>"
- gives each ask the line "Goal (depth N): Root › … › goal"

At boot, `ensureRankSchedule` copies the new prompt onto the live schedule, so the live daily run picks it up after the deploy.

**(b) A new ask is ranked when it is filed.** I chose the cheap rank in code, so the daily cost stays at today's level and no Secretary session runs on filing.
- `createAsk` (ask-verb.ts) calls `rankOnFiling` (asks.ts).
- The ask's goal comes from its target: a grant's goalId, a key result's or retainer's grant, a captain request's goal, a goal proposal's target or parent. Otherwise it is the goal the building is attached to, and failing that the root.
- **The rule a new ask follows:** it goes just below the last live ask whose goal is as near the root or nearer. An older ask at the same depth stays above it. A do ask goes to the bottom, and any other ask goes above the unranked do asks at the bottom.
- All live asks are then numbered 1..n in that order. The Secretary's own order stays as it was.
- Nothing logs `ask.ranked` and no `updatedAt` changes, so the 07:00 run and the decision runs still run and re-rank by the whole rule.

**Tests:**
- A new test in packages/core/test/secretary-rank.test.ts checks: a shallower ask goes above a deeper one; at the same depth the older ask stays above; the Secretary's order stands when a new ask arrives; the read carries the root goal and goal paths; the schedule's prompt contains RANK_RULE.
- In secretary.test.ts, one expected line changed: the brief now shows `#1` on a newly filed ask.
- Core suite: 1097 tests, all green. `npm run check --fast`: one timing test (maxGap < 100 ms) failed on the first run and passed on the rerun.
- I also added one sentence to docs/legible-delegation.md and a new file, docs/log.d/2026-11-19-pix-1-rank-asks-by-the-goal-tree.md.

## What I need from you
Nothing needed.
