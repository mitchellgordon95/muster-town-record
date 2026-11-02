---
id: "dc_wd61y6ekd9"
type: "report"
state: "building"
title: "6c80fe4 live: /api/kpis returns Fund, Join and Trust and the Dashboard opens for guests; the grouped board waits on the Workshop's objectives"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: the Workshop's three objectives are live (dc_y93vhb84ec). The grouped-board check you left open goes to you as a separate assignment."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T07:05:25.797Z"
sessionId: "se_grioeusexw"
assignmentId: "as_5ssi06g7rr"
costUsd: 0.5023869000000001
tokens: 21526
turns: 17
createdAt: "2026-10-27T07:00:20.310Z"
updatedAt: "2026-10-27T07:05:25.797Z"
---
## What I did
Checked the live server (GET /api/health commit 6c80fe4) through the API and a headless guest browser (`/?guest`). Checked the event log to see whether the zero KPIs are real. Answered Pix's question about attaching existing key results. No code changes.

## Findings
- **GET /api/kpis works:** it returns the framing text and kpi_fund, kpi_join and kpi_trust, each with this week, last week, 8 weekly values and a detail line. All three are 0, and that is correct: the 23 bank.input and 13 grant.funded events so far all come from one user, the owner, who is excluded.
- **Dashboard as a guest:** opens from the HUD ▤ button and shows the framing, the 3 KPI tiles and every building's objectives ("No objectives yet (n key results under none)"). There were 0 page errors.
- **Board grouping is not verified yet.** The Workshop board shows kr_vyrhhiyotb with its grant, but no building has entered an objective, so there is nothing to group. GET /api/buildings/workshop/objectives returns `objectives: []` with the KR under `unsorted`.
- **Pix's question (ms_dbdbriql1a):** `set_key_result {id, objectiveId}` changes only objectiveId. The id, status, statusNote and grants stay the same, because grants point at keyResultId. The move logs a kr.updated "moved" event, and `objectiveId: null` moves the KR back. objectives.test.ts covers this. I told Pix how to enter the Workshop's objectives.

## What I need from you
Pix (or Mitchell in Building → Settings): enter the Workshop's objectives with `set_objective` and put kr_vyrhhiyotb under the Trust one. The board then groups its key results.
