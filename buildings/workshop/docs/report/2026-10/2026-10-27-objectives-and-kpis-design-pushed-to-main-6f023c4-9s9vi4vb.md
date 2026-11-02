---
id: "dc_gp9s9vi4vb"
type: "report"
state: "building"
title: "Objectives and KPIs: design pushed to main (6f023c4); build parked until the waiting redeploy"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_akz25kqo2q"],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "No changes from Pix to the Workshop draft objectives or the Trust measure: build what's written (continuation as_dgepcp6k7d resumes on the deploy). Mitchell's markup goes in rollup 18 Needs; existing and new key results start under Unsorted and get attached to objectives after 043 lands."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T06:31:54.842Z"
sessionId: "se_28tscyi9ft"
assignmentId: "as_dgepcp6k7d"
costUsd: 1.0868742000000002
tokens: 48473
turns: 23
createdAt: "2026-10-27T06:10:25.045Z"
updatedAt: "2026-10-27T06:31:54.842Z"
---
## What I did
A redeploy was waiting for my session to end, so I stopped once the design was written and pushed. It's commit 6f023c4 on main. Nothing is built yet.

## Findings
- **The framing** is in `docs/goals.md` (new). The town goal is three town KPIs: Fund, Join and Trust. They are standing indicators that are never met or missed, and they go at the top of a town dashboard. Every building objective names the one KPI it moves. There is no North Star.
- **Data shape** is the "Objectives and KPIs" section at the top of `docs/goal-directed-budgets.md`:
  - Each building gets up to 3 objectives. Each has one sentence, a quarter horizon and the KPI it moves.
  - Key results gain an `objectiveId`, at most 4 per objective.
  - The minimums (2 objectives, 2 key results each) are shown as hints but not enforced.
  - Grants still fund one key result. Lanes, the stoplight and checkpoints don't change, because they all use the key result id.
  - The new `kpis` table is seeded with three rows. Their values are computed from town data each week (this week, last week, and 8 weekly points).
- **The measures.** "Owner" means anyone with a town-wide admin role, which today is Mitchell.
  - **Fund:** humans other than the owner who funded a grant or added Bank tokens, and how many tokens.
  - **Join:** strangers whose first activity was that week and who came back on a later day within 14 days.
  - **Trust:** humans other than the owner who answered an outbox request, or funded a second grant.
  - Expect all three to read close to 0 today, since the town has one funder.
- **Migration path.** Migration 043 only adds things. Existing key results start under "Unsorted" and keep their ids, statuses and grants. Nothing moves under an objective automatically.
- **Workshop draft objectives** (in the doc, for Mitchell and Pix to mark up):
  1. Trust: "a funder can see exactly what every token bought". kr_vyrhhiyotb goes here.
  2. Join: "a stranger finishes useful work in their first session".
  3. Fund: "someone other than Mitchell funds a key result end to end".
  - The other key results under them are suggestions only.

Next session I build it:
- migration 043
- `core/src/kpis.ts`
- the API and the `set_objective` verb
- key results grouped by objective in the desk brief, the board and Settings
- the Dashboard panel

Then I commit to main, redeploy and check it live.

## What I need from you
Mitchell or Pix: mark up the Workshop's draft objectives and the Trust measure in docs/goal-directed-budgets.md if you want changes before I build. Otherwise I'll build what's written.
