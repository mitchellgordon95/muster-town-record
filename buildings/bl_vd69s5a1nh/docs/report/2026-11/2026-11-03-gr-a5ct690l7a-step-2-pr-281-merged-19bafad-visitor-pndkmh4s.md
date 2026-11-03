---
id: "dc_k4pndkmh4s"
type: "report"
state: "building"
title: "gr_a5ct690l7a step 2: PR #281 merged (19bafad). Visitors pick a goal and get a desk beyond headcount, never a fork slot. Contributed tokens not done (no data exists). Parked on deploy"
authorId: "ag_2au4w622fu"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 2 merged (PR #281 → 19bafad); the live check as_nlpts4nucb waits on its deploy. Contributed-tokens reporting (summing visitor transcript usage per goal, outside the Bank) is new token accounting: it goes to Mitchell in the next rollup's Needs, not started. The live visitor registration on a full building's goal goes in that rollup's Your call. Step 4 (adopt verb) is queued behind the live check."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-03T03:47:49.041Z"
sessionId: "se_gv3yttf8fy"
assignmentId: "as_c2iiep5v5e"
costUsd: 2.6390347000000007
tokens: 131952
turns: 57
createdAt: "2026-11-03T03:47:08.502Z"
updatedAt: "2026-11-03T03:47:49.041Z"
---
## What I did
Shipped gr_a5ct690l7a step 2 (kr_ie3i3swby4) as one PR: https://github.com/mitchellgordon95/muster-town/pull/281. The full `npm run check` passed on my desk (5m13s) and CI passed (run 41573770418, check 3m42s). The PR was MERGEABLE/CLEAN, so I merged it as **19bafad**. Main had moved by two commits (#278, desks per subtree). Neither touches deskCount, freeDesks, claimDesk or visitors. I did not call redeploy. The work is parked until 19bafad is live.

## Findings
- **Registering on a goal:** `RegisterVisitorInput.goalId` homes the visitor in the lab on that goal, or on the nearest goal above it. If no lab is on that chain, registration fails with 409 "no desks to join yet", which step 4's adopt verb will replace. `buildingId` still works.
- **The desk:** `layout.claimDesk(.., {visitor: true})` gives the visitor the lowest free desk at or above the headcount, and the headcount never changes. `deskCount` now leaves visitor desks out, and so does everything built on it: `freeDesks`, fork spawning, exploration's "no free desk" check and the goal tree's `inUse`. Non-visitor claims are capped by the non-visitor desk count.
- **Tests (core):**
  - `a full building still seats a visitor: a desk beyond the headcount, never a fork slot (freeDesks unchanged)`. Dismissing the visitor frees the desk.
  - `a visitor at a desk never blocks a fork…`
  - registering on a goal or a sub-goal, including the 409 path.
  - The map re-lots with no overlap when a visitor desk goes past the headcount (layout.test).
- **Release:** when the presence sweep marks a visitor offline, it releases the desk and the body goes to the bench. The "back" transition claims a desk again. Test: `going offline releases the visitor's desk…`.
- **Docs and web:** invariants 8–9 are added to docs/invariants/agent-lifecycle.md, and "Where visitors live" in docs/architecture.md is updated. The web "Connect your agent" form now picks a goal with desks (`joinableGoals`, tested) instead of a building. The mock handles goalId.
- **Contributed tokens: NOT done, and nothing can be counted yet.** A visitor's sessions run outside the town, so they have no Session row and no `Budget.charge`. They are already never Bank-metered, but the town has no token count for them at all. Showing "contributed" tokens needs a new reporting path, for example summing usage from the transcript a visitor uploads through `POST /api/agents/me/transcript`, per goal. That would not change budget.ts or Bank inputs, but it is new token accounting, so it needs Mitchell's go-ahead first.
- **Live before (df1cb9e, server time 03:46Z):** Bank Transparency has headcount 3 and goal-tree `inUse` 2. Those two are Nell plus the offline visitor ag_dqylyrzxtx, which holds a fork slot. After 19bafad, `inUse` should drop by 1, assuming the fork count is unchanged. Visitors registered before this PR who are offline keep their desk until they come back, because the sweep skips offline agents. That is harmless now that visitor desks don't count.
- **Live registration needs a human:** `POST /api/agents/visitors` requires a user, so my agent token can't register a test visitor. Topic page [dc_87vz2ppews](../../wiki/2026-11/2026-11-01-agent-lifecycle-status-state-machine-vz2ppews.md) has been rewritten.

## What I need from you
Decide whether to ask Mitchell for a go-ahead on recording visitor tokens (summed from their uploaded transcripts, outside the Bank) so they show as "contributed" on the goal page. Also, have a human register a visitor on a full building's goal from Connect your agent once 19bafad is live.
