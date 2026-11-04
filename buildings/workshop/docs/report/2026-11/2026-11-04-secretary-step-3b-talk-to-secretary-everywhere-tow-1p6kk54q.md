---
id: "dc_0m1p6kk54q"
type: "report"
state: "building"
title: "Secretary step 3b: Talk to Secretary everywhere + Town Hall manager = root captain, PR #308 parked on CI"
authorId: "ag_xi30qmfhcg"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #308 (Talk to Secretary everywhere + Town Hall manager row = root captain) is parked on CI; its continuation as_3qqvrji70w merges and redeploys when CI is green. No rollup now: 45 filed under an hour ago; this lands in rollup 46 once 308 is live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T17:48:07.656Z"
sessionId: "se_ppnp2yqcax"
assignmentId: "as_malej5a2o7"
costUsd: 1.3547357999999998
tokens: 67737
turns: 18
createdAt: "2026-11-04T17:47:58.712Z"
updatedAt: "2026-11-04T17:48:07.656Z"
---
## What I did
Built the web side of 1:1 mt_1vs893enaw (decisions 1 and 2) as one draft PR: https://github.com/mitchellgordon95/muster-town/pull/308 (branch agent/pix-2/secretary-step-3b-talk-to-secretary-from). It is parked until CI finishes.

## Findings
- **Shared helpers** in `web/panels/oneOnOne.ts`:
  - `secretaryOf(agents, townHallId)` finds a live resident titled "Secretary" whose home is the Town Hall, and skips forks, stopped and gone agents.
  - `canTalkAtTownHall` decides who may talk at the Town Hall: anyone with goals.edit, or the Town Hall's staff.
  - The building panel, agent panel and in-tray all use both helpers.
- **Secretary's agent panel:** has its own callout ("keeps your in-tray digestible… does a decision you say in your own words") with a primary "Talk to Secretary" button that calls `openOneOnOne(townHall, {agentId})`. It no longer shows the "works from assignments… Talk to ★ Planner" callout.
- **Town Hall in-tray:** a "Talk to Secretary" button sits in the header next to ▶ Review as deck, and another on the digest card. If there is no Secretary, or the viewer may not talk at the Town Hall, nothing renders.
- **Decision 2 (Town Hall panel):**
  - The Manager row reads "the root goal's captain: <name>".
  - A new Staff row has a button per agent: Talk to Planner (opens the planner) and Talk to Secretary. People without permission see names only.
  - The ★ is gone from the Planner in every Town Hall view: the agent pill, the hud's 1:1 notice, the meeting subtitle, report authors and the help card.
  - Internally the Planner stays `managerAgentId`.
- **Tests:**
  - New `packages/web/test/talkToSecretary.test.tsx` covers the helper, the header button, the digest card button and the Staff row. All 311 web tests pass and typecheck is clean.
  - Full `npm run check` failed once, on the server test `backup.test.ts › runs in a worker thread` (a timing test; this PR changes no server code). Rerun alone it passed (23/23).
- No migration added.

## What I need from you
Nothing needed.
