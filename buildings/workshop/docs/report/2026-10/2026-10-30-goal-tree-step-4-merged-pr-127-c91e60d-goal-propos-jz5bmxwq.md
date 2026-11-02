---
id: "dc_gmjz5bmxwq"
type: "report"
state: "building"
title: "Goal tree step 4 merged (PR #127, c91e60d): goal proposals in the in-tray and deck, Mine/All, owner decide, read-only Spend tab; live check parked"
authorId: "ag_x0xbpvumtr"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 4 merged as c91e60d (PR #127), no migration, no Bank write, CI green. Live check as_uqzljybep5 is already queued on deploy c91e60d; nothing else to add. Goes into rollup 33 as part of the goal-tree Shipped item."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T23:06:56.758Z"
sessionId: "se_bunrl040cc"
assignmentId: "as_ic5rj33cho"
costUsd: 4.0988512
tokens: 204943
turns: 68
createdAt: "2026-10-30T23:06:46.603Z"
updatedAt: "2026-10-30T23:06:56.758Z"
---
## What I did
Built step 4 of docs/goals.md. It is in PR #127 (https://github.com/mitchellgordon95/muster-town/pull/127), merged as **c91e60d** after CI passed, and I queued the redeploy. No migration (main's highest is still 061) and no Bank or token-accounting change. I updated the docs/goals.md "Built" marker, docs/log.md and topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md).

## Findings
- **Goal proposals in the Town Hall in-tray:** open proposals from propose_goal / propose_key_result now appear in the Town Hall in-tray list (`goalProposals`) under a "Goal proposals" section. Each has the editor's Accept / Edit and accept / Cut, using the same decide route, and a cut sends the note to the proposer. The badge counts them and refreshes on `goal.proposal` events.
- **Goal proposals in the deck:** the review deck gets one `goal-proposal` slide per open proposal, after the grant proposals (the doc's order).
- **Mine / All:** each in-tray item is routed to the owner of its goal (core `intray-routes.ts`, using Goals.route). The in-tray and `/api/review-deck` responses now tell each viewer which items are theirs ("Mine") and which they may decide. A signed-in human gets a Mine / All toggle that filters both the list and the deck.
  - An owner who is not an admin starts on Mine; admins start on All.
  - An admin's Mine holds the items routed to the root goal (owned by the town admins).
- **Owner decide on grants:** a goal's owner now sees the decide buttons on grants in their subtree (Fund / Counter / Reject, Continue / Adjust / Cut, Mark met), plus a "For <owner>" line. The web shows the buttons only where the server would allow the action (Grants.canFund). Member funding is unchanged.
- **Spend tab (read-only):** a third tab on a goal in the Goal tree, served by `GET /api/goals/:id/spend?days=7|30|90` (core `goal-spend.ts`). For the goal and everything under it, it shows adjusted tokens:
  - by lane;
  - by day (windows up to 14 days) or by week;
  - by building and by key result;
  - next to the key results marked met or missed in the window.
  
  Each session counts toward a goal by its lane: a grant session toward its key result's goal, a session naming a key result toward that key result's goal, anything else toward its building's goal. It reads only session rows and never needed a Bank write. A test checks that the Bank balance, the grant and the event log are unchanged after it runs.
- **Tests:** new core tests in `goals-step4.test.ts` and web tests in `goalsStep4.test.tsx`. Full `npm run check` passed (core 505, web 159 and the other suites) and CI passed.
- **Left out:**
  - the per-user review marker (`lastReviewedAt` per human, "decided by Lena");
  - the Finance panel's by-goal view;
  - the grant panel's goal path and "under review" pill.
  
  The state-of-the-town slide already had no dials, so nothing changed there.
- **Not exercised live yet:** a non-admin owner and the decide buttons on the live town, because there is no second human owner and my desk is a guest.

## What I need from you
Nothing needed.
