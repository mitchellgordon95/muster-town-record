---
id: "dc_30ydg6hj3c"
type: "report"
state: "building"
title: "Objectives and KPIs built and pushed to main (6c80fe4): objectives hold key results, Fund/Join/Trust on a new Dashboard; parked for live check"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved; your parked continuation (live check of 6c80fe4) resumes by itself. I take entering the Workshop's objectives and moving kr_vyrhhiyotb under Trust as my own assignment after the deploy."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T06:58:34.480Z"
sessionId: "se_fgyv5bov3i"
assignmentId: "as_g943yt9cr4"
costUsd: 4.670732999999999
tokens: 365037
turns: 88
createdAt: "2026-10-27T06:45:47.721Z"
updatedAt: "2026-10-27T06:58:34.480Z"
---
## What I did
I built the design from 6f023c4 and pushed it straight to main as **6c80fe4**. I also requested a redeploy, so 6c80fe4 should be the live commit once this session ends. No PR, per the Workshop's standing rule. Nobody has marked up the draft objectives, so I built what was written.

## Findings
- **Data (migration 043, additive):**
  - New `objectives` table: text, quarter horizon, the KPI it moves, who wrote it and the sources.
  - New `kpis` table, seeded with Fund, Join and Trust.
  - `key_results` gains `objectiveId`.
  - Existing key results land in "Not under an objective yet". Grants, lanes and the stoplight are unchanged.
  - Limits: at most 3 objectives per building and 4 key results per objective. A 4th objective or 5th key result is refused.
- **KPIs (`core/src/kpis.ts`):** computed live over 8 weekly windows, never typed in. Anything done by town admins is left out, because the KPIs measure strangers.
  - Fund: funders other than the owner (grants funded or Bank inputs added).
  - Join: newcomers who came back on a later day within 14 days.
  - Trust: humans who answered an outbox request, or funded a second grant.
- **API and verbs:**
  - `GET/POST /api/buildings/:id/objectives`, `PATCH/DELETE /api/objectives/:id`, `GET /api/kpis`.
  - New manager verb `set_objective`; `set_key_result` takes `objectiveId`.
  - Moving a key result between objectives shows up in the manager's in-tray as "moved".
- **Views:**
  - The desk brief, the building board and Building → Settings ("Objectives and key results": a KPI picker and a "Move under…" select) all group key results under their objectives.
  - New **Dashboard** panel, opened from the HUD ▤ button or Town Hall → Settings: the framing paragraph, three KPI tiles (this week, last week, an 8-week sparkline, the measure) and every goal-directed building's objectives.
- **Checks:**
  - Typecheck passes in all packages.
  - Tests pass in core (331), server (99), web (74) and runtime (130). New tests: `core/test/objectives.test.ts` and the objective groups in `web/test/keyResults.test.ts`.
  - I ran the mock UI with Playwright and looked at screenshots of the Dashboard, the grouped board and the Settings editor: no page errors.
- **Fixes made along the way:**
  - Root's ee536a5 had left the web mock returning a single `proposal` instead of `proposals[]`, which failed one web test. Fixed.
  - `v12.test.ts` needed the new tables dropped from its fake old database.
- **Not done yet:**
  - **Not checked live yet.** That waits for the redeploy.
  - The Workshop's real objectives haven't been entered, so kr_vyrhhiyotb is still unsorted.

## What I need from you
Pix or Mitchell: enter the Workshop's objectives (draft in docs/goal-directed-budgets.md) with `set_objective` or in Building → Settings, and put kr_vyrhhiyotb under the Trust one.
