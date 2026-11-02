---
id: "dc_jaii2zxeqb"
type: "report"
state: "building"
title: "Goal tree step 3 merged (PR #125, b01e71d): the Town Hall goal editor; live check parked"
authorId: "ag_cx6ytg2uqo"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Step 3 (Town Hall goal editor) merged as PR #125 b01e71d, no migration, no Bank code; the parked continuation as_xjnw7nmrv2 does the live check and the editor screenshot for rollup 33. Step 4 queued separately, waiting on that live check."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T22:44:19.324Z"
sessionId: "se_afg3ngfzd8"
assignmentId: "as_4yop6brb1z"
costUsd: 3.9038465999999987
tokens: 195192
turns: 72
createdAt: "2026-10-30T22:43:58.155Z"
updatedAt: "2026-10-30T22:44:19.324Z"
---
## What I did
Built goal tree step 3 (docs/goals.md, "The Town Hall goal editor"). It's merged as PR #125 (https://github.com/mitchellgordon95/muster-town/pull/125). The merge commit is **b01e71d** on main. CI passed and `npm run check` passed locally. I queued the redeploy, so **b01e71d should be live** after the restart. I haven't seen it live yet; the parked continuation checks it and takes the screenshot. I also updated topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md) and the docs (goals.md step 3 "Built", architecture.md, manual.md, log.md). There's no migration and no Bank code.

## Findings
**What a signed-in admin sees.** The Town Hall has a new **Goal tree** wall chart on its back wall, above the map table. It's place `goal-tree`, `TILE.GOAL_CHART`, and walking up to it lists it in `look`. Press E there to open the Goal tree panel:
- **Proposals** (top, when there are any): open `propose_goal` / `propose_key_result` items. Each shows its path, old → new words, the proposer and their building, and the why. A proposal from outside the proposer's subtree is flagged. The buttons are **Accept**, **Edit and accept** (words, plus how-to-check and due for a KR) and **Cut** (the note goes to the proposer's inbox). They use the step 1 decide route, which already sends that inbox message.
- **Tree**: one row per goal, indented, with an owner pill and attached-building chips. Under each goal are its KR lines: status pill, due date (amber when past due), and "funded" (links to the grant) or "open". Met and missed KRs fold into "✓ n done, m missed". There's a **Show retired** toggle and a building filter that dims goals outside that building's subtree.
- **Goal detail** (click a goal): breadcrumb, words, owner (own or inherited), attached buildings. Admins and owners get these buttons:
  - **Edit**, **Add goal**, **Add key result** (text, how to check, due, building).
  - **Move**: never under its own subtree.
  - **Owner**: any user who holds a role, or inherit.
  - **Retire**: lists the open KRs and attached buildings that must move, with a sibling picker. The button stays disabled until a sibling is picked, and the server also refuses without one.
  - **Met / Missed** on each open KR.

  Below that are a **History** tab (new `GET /api/goals/:id/history` = `Goals.history`: goal, KR, attachment and proposal events from the event log, newest first) and a **Subtree** tab (buildings below, open KRs by due date).
- **Without `goals.edit`** at a node (guests, members, a non-owner), the same tree is read-only. The server checks permissions again on every write.
- The building **Overview** now shows "Reports to <owner> via <goal>"; the goal opens the tree at that node. The building Goals tab and the Dashboard link to the tree.
- **The map redraws** after editor writes: they go through `Goals.create/update/retire`, whose `goal.created/edited/moved/retired` events trigger step 2's rebuild hook (world.ts:196).

**Tests:**
- core `goals.test.ts`: History includes its own goal and KR events but not a sibling's; the wall chart sits on the back wall with a walkable stand.
- web `goalTree.test.ts`: rows and Show retired, archived folding, past due, `canEditGoal` (admin, owner in subtree, guest), the retire plan's siblings, move targets, the building filter, and which goal a proposal belongs to (mirrors core `nodeOfProposal`).

**Left out:**
1. The building Goals tab keeps its old editor instead of going read-only. Removing it would also drop KR Delete, which the new editor doesn't have. `set_objective` / `set_key_result` are unchanged: still working, still mirrored into the tree, nothing added.
2. The tree has no "proposed" grant word; it shows only funded / open.
3. There's no Attach control on the goal; it stays in building Settings.
4. Plan with an agent is step 5.

**Next session (parked on deploy b01e71d):**
- Health commit includes b01e71d.
- `look` lists `goal-tree`.
- `GET /api/goals/gl_workshop/history` returns events.
- The bundle contains "Goal tree".
- Screenshot the editor (mf_) for rollup 33 (topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md) has the method). A desk is a guest, so it shows the read-only tree.

Step 4 comes after: in-tray/deck goal proposals, Mine/All, owner Fund, Spend tab.

## What I need from you
Nothing needed.
