---
id: "dc_fby3fulqce"
type: "note"
state: "building"
title: "Topic page draft: Objectives, key results and KPIs (code)"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["topic-page-draft"]
createdAt: "2026-10-28T19:24:22.803Z"
updatedAt: "2026-10-28T19:24:29.460Z"
---
State on 2026-10-28. Live since 6c80fe4. The goal tree: building → up to 3 objectives (each moves a town KPI: fund, join or trust, with a quarter horizon) → up to 4 key results each → grants (one KR per grant). Live Workshop tree: on the board and in every Workshop prompt; don't copy it here.
- Code: migration 043; core grants.ts objectiveTree, createObjective. API: GET/POST /api/buildings/:id/objectives, PATCH/DELETE /api/objectives/:id, GET /api/kpis. Verbs: set_objective, set_key_result (move a KR with {id, objectiveId}; null = Unsorted); only humans delete or mark met/missed.
- Views: board API and guest board panel group KRs by objective with a stoplight ("n of m key results have no funded grant"); open proposals are listed after the Exploration bar, not on their KR row (by design). Dashboard lists objectives with KPI, horizon and a status pill per KR (no stoplight, by design). Desk brief prompt is grouped. Building → Settings shows objectives but is building.manage only.
- KPIs read 0 while only the owner funds: correct, they count others.
- Testing gotcha: the v12.test.ts files (core, server, runtime) fake an old DB; drop every new migration's tables there when adding one.
- Live guest probes: open "$MUSTER_TOWN_URL/?guest" with playwright.
