---
id: "dc_3xz7obkbpv"
type: "report"
state: "building"
title: "Goal owner → captain rename: PR #183 open, all packages green; parked on CI"
authorId: "ag_flxwiusq28"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_3jtclcoxl2","dc_hai9ky5u7a"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/183"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #183 (d3fc02f) owner → captain in every human-facing place, no migration, API names kept; continuation already parked on CI (merge, redeploy, live-check \"Set captain\" in the bundle, line on dc_hai9ky5u7a). Once live I reword kr_j1w17nw178 and gr_bwm0iz7rwl to \"captain\" myself."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T20:31:08.599Z"
sessionId: "se_wzi7co5q9j"
assignmentId: "as_4xi0q1s3xe"
costUsd: 1.7926193000000004
tokens: 89631
turns: 42
createdAt: "2026-10-31T20:30:59.352Z"
updatedAt: "2026-10-31T20:31:08.599Z"
---
## What I did
I grepped "owner" (case-insensitive) across packages/ and docs/ and changed every place where a human reads a goal's owner to say **captain**. That change is commit d3fc02f on PR https://github.com/mitchellgordon95/muster-town/pull/183 (draft). CI was pending at 20:30Z. Before pushing I ran `npm run typecheck`, then vitest one package at a time: core 531, server 225, runtime 187, desk 38 and web 187 tests passed. I updated 4 core test regexes to match the new error wording. check:docs and check:deadcode passed. I took a crop from the mock UI: mf_nfkqlzy6nu (goal detail showing "Captain: the town admins" and a **Captain** button). I added a Shipped-candidate line to "Rollup 35 materials" ([dc_hai9ky5u7a](../../wiki/2026-10/2026-10-31-rollup-35-materials-i9ky5u7a.md)) before 21:50Z.

## Findings
- **Changed:**
  - **Goal tree:** the tag tooltip, the "Captain: …" line in the detail, the toolbar button, and its form (label, hint, "Set captain"). The line now reads "Only an admin or this goal's captain edits it".
  - **Building Overview:** "Captain: <name> · in the goal tree →" and the Attached-to hint.
  - **In-tray:** the Mine tooltip ("the goals you captain") and the funding note.
  - **Core messages:** error and event texts in goals.ts and goal-changes.ts ("Only an admin or the captain of …", "Captains are humans", "X captains …"). The Planner prompt's tree lines now read "(captain …)".
  - **Desk brief:** "Attached to: … (captain: the town admins)" and the grants block.
  - **MCP tool:** the propose_goal description.
  - **Docs:** docs/goals.md (the section is now "Captains on nodes", with a note on the naming) and docs/how-work-gets-done.md.
- **Kept on purpose:** `goals.ownerId`, the API `owner` field, the `goal.owned` event type and internal identifiers. No migration and no API rename.
- **Left alone (not goal owners):**
  - the town owner in the KPIs ("other than the owner")
  - a Bank input's or subscription's owner ("My subscription (owner)")
  - a visitor agent's owner and its permissions
  - a hosted collective's owner
  - the repo owner in URLs
  - "Team owners" (billing) in the manual
  - docs/log.md history, and "owner" meaning a building or a step in design.md and waterfall.md
- **Manual:** no goal-owner wording, so no change. It is at 1894 of its 1900-word cap.
- "Ask to own" is not in the code yet. The text of kr_j1w17nw178 and gr_bwm0iz7rwl still says "ask to own" and "owner"; Pix should reword it. When that feature is built, its button should say "Ask to captain".
- **Desk mishap, fixed:** a `git stash` with nothing to stash followed by `pop` applied an old auto-stash. I reset the tree to d3fc02f, and all 8 stash entries are still there.
- **Plan for the next session:**
  1. Check CI with `gh pr checks 183`.
  2. Mark the PR ready and merge it, with a merge commit.
  3. Redeploy.
  4. Park with resumeWhen {deploy: merge sha}.
  5. Live check: grep the bundle under /workshop/assets/main-*.js for "Set captain".
  6. Update the PR #183 line on [dc_hai9ky5u7a](../../wiki/2026-10/2026-10-31-rollup-35-materials-i9ky5u7a.md). If it is past 21:55Z, say so in the report instead.

## What I need from you
Nothing needed.
