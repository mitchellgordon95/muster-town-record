---
id: "dc_prbldpn6ph"
type: "report"
state: "building"
title: "Goal tree editor UX pass: a sheet over the map with tree nodes and the Planner 1:1 beside it (PR #152, 44032d8, redeploy queued)"
authorId: "ag_d02zoj8ffj"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #152 merged as 44032d8, redeploy queued; your live check as_4mqk3814io already waits on deploy 44032d8. For the rollup I'll use the \"after\" crop mf_sszvose9rk. Known gaps (Planner 1:1 fixed to its opening goal, WASD moving the avatar under the sheet) stay as notes unless Mitchell asks."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T03:01:01.549Z"
sessionId: "se_7967y4fut1"
assignmentId: "as_e08cjzwqgi"
costUsd: 3.2039565000000008
tokens: 160198
turns: 69
createdAt: "2026-10-31T03:00:47.737Z"
updatedAt: "2026-10-31T03:01:01.549Z"
---
**What Mitchell now sees:** clicking the Goal tree opens a large sheet over the map instead of the narrow side panel. On the left is the tree as nodes you can collapse. Each node shows its buildings, owner, "n KR · m funded", how many are late (or the next due date) and "n proposals" waiting. Each open key result sits under its goal on one line with a status dot. On the right is the selected goal: its words, a row of small buttons (Edit words, + Goal under it, + Key result, Move, Owner, Change this goal, Retire), the proposals waiting there with Accept / Edit and accept / Cut, and the key results as cards with "how to check". **Talk to the Planner** opens his 1:1 in the side panel next to the sheet, and the sheet stays open while he talks.

## What I did
- Took screenshots of the editor on mock data, signed in as Mitchell, with the live goal tree loaded. Listed what was wrong, then went through build → screenshot → adjust 5 times.
- Shipped it as PR #152 (https://github.com/mitchellgordon95/muster-town/pull/152). CI was green and I merged it as **44032d8**, then queued a redeploy. **44032d8 should be live** once the server restarts. I haven't live-checked it yet.

## Findings
The worst problems before the change (crop below, mf_qx1eaggda3):
1. Everything was squeezed into a ~500 px side panel. The proposals came first and pushed the tree off the screen.
2. Opening a goal *replaced* the tree, so you lost your place and had to click "← Tree" to get back.
3. Seven big decide-footer buttons, plus huge Accept / Cut buttons, took up most of the panel.
4. There was a "Plan" button on every row, and you couldn't collapse anything or see a goal's status at a glance.
5. "Plan with an agent" swapped the editor out for the meeting, so you couldn't chat and edit at the same time.

Which of Mitchell's three ideas I used:
- **Main modal: kept.** It's a sheet over the map, placed to the left of any side panel. Links to a grant, a building or the 1:1 open in the side panel and leave the sheet open. × closes it, and so does Esc when no side panel is open.
- **Tree node display: kept.** Nodes have collapse/expand, tags you can read at a glance, and a highlight on the selected goal. Proposals now show at the goal they belong to: the root lists all of them, other goals list their own and those below.
- **Chat on the side: kept, without new chat code.** The Planner's 1:1 opens in the normal side panel beside the sheet, so it reuses the full meeting view (transcript, decisions, the proposal cards the Planner attaches). No second assignment is needed.
- **Dropped:** the "Plan" button on every row (one button in the header does the job) and the "Goals under it" section (the tree already shows them).

![After (preferred for the rollup): tree nodes on the left, the selected goal and its waiting proposal on the right](/api/media/mf_sszvose9rk.png)
![Before: the side-panel editor, with the goal's detail replacing the tree and big buttons](/api/media/mf_qx1eaggda3.png)

How I checked it:
- `npm run typecheck`, the web tests (180 passed, including new ones for `visibleRows` and `nodeGlance`), check:docs and knip all pass, and CI is green.
- The screenshots come from the mock web build: `VITE_MOCK=1`, Mitchell signed in, the tree from the live `/api/goals`. The "after" crop uses a made-up proposal.
- In mock mode, the Planner button now opens a 1:1 with a building manager so the flow can be demoed.

Known gaps:
- The Planner 1:1 stays on the goal it was opened from. Picking another goal doesn't change what the Planner is looking at.
- Keys like WASD still move the avatar on the map while the sheet is open. The manual sheet has the same behaviour.
- Nobody has tried it signed in on the live town yet.

Topic page: [dc_hsq0e5a587](../../wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md).

## What I need from you
Nothing needed.
