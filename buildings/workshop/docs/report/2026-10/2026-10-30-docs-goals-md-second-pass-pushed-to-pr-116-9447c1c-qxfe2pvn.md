---
id: "dc_j9qxfe2pvn"
type: "report"
state: "building"
title: "docs/goals.md second pass pushed to PR #116 (9447c1c): owners, reorg, budget by node, KPI slides, skip-level, postmortems, kanban"
authorId: "ag_isiby9rsh1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_a3nvwfawer","dc_9pz8e24o41","dc_0xqyrevla1"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/116"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Second pass done as decided in 1:1 mt_a3nvwfawer (decision 2). PR #116 at 9447c1c is ready for Mitchell; the 9 open questions go to him in rollup 31. Nothing further queued until he answers."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T18:21:31.226Z"
sessionId: "se_ysd4lryfol"
assignmentId: "as_bb0wrwf0v7"
costUsd: 1.1181682000000002
tokens: 55908
turns: 17
createdAt: "2026-10-30T18:21:12.798Z"
updatedAt: "2026-10-30T18:21:31.226Z"
---
## What I did
I rewrote docs/goals.md on the PR #116 branch and pushed it as commit 9447c1c (I checked it on origin; the PR head is 9447c1c). It is design only, with no code. The doc adds the 7 requested sections and tightens the first pass rather than just appending. I also updated the topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md). PR: https://github.com/mitchellgordon95/muster-town/pull/116

## Findings
- **Length.** The doc is about 4,600 words, up from 3,163 in the first pass: roughly 15 minutes at a brisk read, up to 18 at a slower one. A new scope note at the top records Mitchell's reflection that this is turning into an org/corporation sim. It borrows only an owner per node, one reorg action and a board view of the queue. It adds no ceremony: the morning and evening review is the iteration.
- **Owners.**
  - Data: a new `goals.ownerId` field, holding a user now and able to hold an agent later. A node with no owner inherits from the nearest owned ancestor; the root belongs to the admins.
  - Org chart: drawn from the tree, not declared.
  - Routing: each Town Hall item goes to the owner of its node. A grant goes by its KR's goal, a rollup by the building's attachment, and a building with several attachments goes to the nearest common owned ancestor. The in-tray gets "Mine / All".
  - Powers: an owner can edit only inside the subtree they own.
  - With one human nothing changes: the migration owns only the root.
- **"Change this goal" (the reorg).**
  - Data: a new `goal_changes` table.
  - The human's X→Y note is filed as a doc. That note is the human source for the work it starts, so the lane rules need no change.
  - It schedules a planning meeting at the Town Hall, facilitated by Planner because the Town Hall has no manager.
  - Every building under the node gets one directed assignment.
  - Open KRs get `underReviewSince` and their grants keep running.
  - Proposals accepted at the meeting become the node's new children.
  - It is the only scheduled meeting kind. The doc says the building standup, retro and planning meetings go.
- **Budget by node.** It comes in two halves:
  - A read-only Spend tab that splits existing Bank spend by node, according to each session's lane. This needs no Bank change.
  - Allocating Bank shares to goals the way pools work today, so money moves with a reorg. This is a Bank change: it is marked gated on Mitchell and kept out of the build order.
- **Review deck (kr_2qg0ayfs1j).** One slide per KPI dial, using the 8 weekly points `GET /api/kpis` already returns, plus the KRs that target the dial. A dial with no KR targeting it is called out. These slides come after slide 1 and before the decision slides.
- **Postmortems.** Marking a KR missed asks for a one-line why. That line is the human source, and it queues one small directed postmortem. The postmortem report links to the archived KR.
- **Skip-level.**
  - "Talk to a resident under this goal" opens a 1:1 through the existing `createOneOnOne` route.
  - Catch, found in the code: a fork can't hold a 1:1. `oneOnOneTarget` sends a 1:1 with a fork to its manager, and most residents are now forks.
  - So the doc proposes a new "conversational fork session" that speaks for one recent chain of work. This is open question 8.
- **Kanban.**
  - Columns Queued / Held / Running / Done, built from the existing assignments with no schema change.
  - The WIP limit is the building's desks (`headcount`).
  - It is a Queue tab on the building panel and on a goal node (rolled up with building swimlanes). It is read-only.
- **Build order:** 1 core + owners, 2 editor, 3 in-tray and deck + KPI slides, 4 reorg + Planner, 5 postmortems + kanban, 6 skip-level, 7 new dials. Budget by node sits outside the order.
- **Open questions:** there are now 9. The 4 new ones are: what owners can do (including funding and agent owners), how far ahead the reorg meeting must be, skip-level when a subtree is all forks, and whether to allocate by node at all.

## What I need from you
Mitchell: read PR #116 and answer its 9 open questions; the build waits on that.
