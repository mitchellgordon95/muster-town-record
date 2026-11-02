---
id: "dc_35qw9pbt5t"
type: "report"
state: "building"
title: "The goal tree now shows desks per goal, totalled up each branch; the deck's first slide lists desks by pillar (PR #156, 441f52e, redeploy queued)"
authorId: "ag_0hlsy4lsn3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_n25udpflus","dc_hsq0e5a587"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/156"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #156 merged 441f52e; included in e97dd9c. Live check covered by the e97dd9c check. Rollup 34: desks per goal, crop mf_ug5j4frul5."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T05:01:28.849Z"
sessionId: "se_wwdm1t6cbm"
assignmentId: "as_ocaorgwz9f"
costUsd: 1.5705317999999997
tokens: 78527
turns: 46
createdAt: "2026-10-31T04:57:59.536Z"
updatedAt: "2026-10-31T05:01:28.849Z"
---
## What I did
Once 441f52e is live, Mitchell will see a desk count on every goal in the goal tree sheet. Each node gets a green "n desks" tag: the headcount of every building attached at that goal or anywhere below it. A goal nobody works on gets a muted "0 desks". I chose the muted tag over showing nothing so that unworked goals stand out. Clicking a goal opens the detail pane, where each attached building appears as "Town Workshop · 5 desks". Under that is the line "n desks work this goal (x attached here, y below) · k in use now"; on the root it reads "n desks in the town". Slide 1 of the Town Hall review deck also gains a line: **Desks by pillar:** Fund n · Steer n · Trust n.

Live desk numbers, taken before the deploy from /api/goals plus each building's headcount:

| Pillar | Desks | Buildings |
|---|---|---|
| Fund | 0 | none |
| Steer | 11 | Town Workshop 5, Onboarding 3, UI / UX 3 |
| Trust | 6 | Prod 2, Bank Transparency 2, Code Legibility 2 |
| Root | 1 | Town Hall |
| **Town** | **18** | |

PR: https://github.com/mitchellgordon95/muster-town/pull/156. CI passed, I merged it as **441f52e** and queued a redeploy; 441f52e should be live after it. Crop (mock data): ![goal tree desks](/api/media/mf_ug5j4frul5.png)

## Findings
- **API:** GET /api/goals now gives each attached building `headcount` and `inUse`. `inUse` is `min(headcount, layout.deskCount)`, the same count `freeDesks` in forks.ts uses. The change is additive in core `GoalNode` and schema `GoalTreeNode`.
- **Web:** `subtreeDesks` and `deskWord` sit in panels/goalTree.ts. The tree tag, the detail line and building chips are in GoalTreePanel.tsx, and the Subtree tab chips show desks too.
- **Deck:** "Desks by pillar" added only a few lines to review-deck.ts. It adds "at the root n" whenever a building, such as Town Hall, is attached at the root, so on live data the line will end "at the root 1".
- **Tests:** I extended the core goals.test.ts tree test and the review-deck slide 1 test, and added a web goalTree test for the subtree totals. `npm run check --fast` passed locally and CI passed.
- **Not yet checked live:** I haven't seen the deployed sheet or deck line. The crop is from the mock server.
- I rewrote the topic page [dc_hsq0e5a587](../../wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md).

## What I need from you
Nothing needed.
