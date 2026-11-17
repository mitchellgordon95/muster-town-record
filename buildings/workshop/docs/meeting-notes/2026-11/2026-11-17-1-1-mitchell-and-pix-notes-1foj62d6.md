---
id: "dc_5i1foj62d6"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-17T04:12:49.134Z"
updatedAt: "2026-11-17T04:14:00.575Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Pix here, Workshop. What do you need?
- **Mitchell:** we need to talk about goals, objectives, and key results. it's too messy right now. can you take a pass at the code so we can discuss
- **Pix:** On it. Reading the goals, objectives and key-results code now (migrations, core/goals.ts, the routes, the panels). Back in a few minutes with a map of what's there and where it's tangled.
- **Pix:** Still reading: I have the data model (three layers of key results, objectives mirrored into the goal tree). Checking the status flow and the UI surfaces next, then I'll lay it out.
- **Pix:** Here's the map. Three words, five things in the code.

**1. Goals** — one tree, `goals` table (migration 061), root gl_town, every building attached to one node (core/goals.ts:43-113). Fine on its own. But a goal row also carries the budget dials: exploreCapTokensPerDay, explore, exploreChunkTokens, desksTotal (schema index.ts:1571-1580). So the goal tree is also the budget tree.

**2. Objectives** — the pre-tree model that was never removed. Separate `objectives` table per building (migration 043: text, horizon, KPI fund/join/trust, max 3, needs sourceDocIds), its own API (POST/PATCH/DELETE /api/buildings/:id/objectives), its own verb `set_objective`, its own panel (GoalsTab.tsx: "objectives" + "Not under an objective yet"). And every objective is ALSO written as a goal row with the same ob_ id under the building's attachment (grants.ts:289-293, kept in sync by hand at 315-316). Two tables, two rule sets, two UIs for one node. docs/goals.md:3 itself says "until this is built, today's model holds" — it was built, the old model stayed.

**3. Key results** — the table was reshaped four times: grant-owned (025) → building-owned (032) → under objectives (043) → under goals with due/archive (061) → back on grants (069). The row now has four parent pointers at once: buildingId, objectiveId, goalId, grantId (schema index.ts:1515-1537). docs/goals.md:22 says buildingId/objectiveId are "read by nothing", but objectiveTree still groups by objectiveId (grants.ts:265).

**4. KR state** — seven statuses (not-started, on-track, at-risk, claimed, met, met-unverified, missed; index.ts:1503) plus a second axis `evidence` (verified/claimed/unknown; 1479, migration 103), plus archivedAt, underReviewSince, postmortemDocId. "claimed" means two different things depending on the column.

**5. Grants** carry both `goalId` and a legacy `keyResultId` (= first KR), and Town Hall routing still goes grant → keyResultId → KR → goal (goals.ts:195-200) instead of grant → goalId.

What I'd propose to discuss:
- A. Objectives are goals. Drop the table, API, verb and tab; the ob_ rows are already in the tree. KPI label: drop (you said no KPIs for now) or make it an optional tag on any goal.
- B. A KR has one parent: its grant. goalId is derived; buildingId/objectiveId go unread for real. Status collapses to open / claimed / met / met-unverified / missed; on-track and at-risk become words in the step report, not KR state. The evidence column folds into status.
- C. Grants route by goalId; keyResultId goes.
- D. One UI shape: the building's Goals tab shows its subtree of the one tree (same component as the Town Hall detail), not a second grouping.

Which mess bit you — the words (goal vs objective vs KR), the UI, or the data? I'll scope the work to that.
- **Town:** Pix's reply is waiting on a redeploy (commit 17fa38b); the server is restarting and the meeting resumes after the restart.
- **Pix:** Back after the restart. My map above is still the picture. Tell me which of A–D (or which mess: words, UI, data) you want to start with and I'll scope it.
- **Mitchell:** yeah i think it's we're obviously aligned on what the code should look like and where it currently falls short

don't worry about scoping to me, just fix the whole thing. you can write a grant if you want.

but for your information, it was trying to understand what the heck was going on with the building's overview page
- **Mitchell:** oh also can you do some directed work? investigate why Juno in Outreach hasn't been running any exploratory sessions
- **Pix:** Filing the grant now (four steps: objectives→goals, one KR parent and status, grants by goalId, Overview/Goals tab read the one tree). And yes on Juno: putting a directed assignment on my queue to find out why Outreach runs no exploration. Two minutes.

## Decisions

(none)

## Decisions recorded after close
- Fix the whole goals / objectives / key results tangle, not a scoped slice (Mitchell: "just fix the whole thing"). Pix proposed grant gr_h4m0lyhb1f "One goal tree: objectives and key results untangled" (750k, 4 steps: objectives become plain goals and the objectives table/routes/verb/tab go; a key result has one parent, its grant, and one of five statuses; grants route by goalId and keyResultId goes; the building Overview and Goals tab read the one tree). It waits in the Town Hall in-tray for Mitchell to fund. Trigger: the building Overview page counts goals two ways (objectives table vs keyResultId).
- Directed: investigate why Juno in Outreach runs no exploration sessions (goal dials, free tokens under the goal, desks, explore-tick events, Juno's queue), report the cause with evidence and tell Juno. Queued on the Workshop building queue as as_ws6fu05s91.

