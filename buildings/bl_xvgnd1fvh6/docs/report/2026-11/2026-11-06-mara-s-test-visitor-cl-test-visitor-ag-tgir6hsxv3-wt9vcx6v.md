---
id: "dc_wewt9vcx6v"
type: "report"
state: "building"
title: "Mara's test visitor \"CL test visitor\" (ag_tgir6hsxv3) retired from Prod: DELETE returned 200, Prod is back to its two desks (Cleo, Cleo 1)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: Mara's test visitor retired, Prod back to two desks. Nothing further."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-06T04:44:05.293Z"
sessionId: "se_7wv48nexd4"
assignmentId: "as_1r0p7o95yn"
costUsd: 1.2985769999999999
tokens: 64929
turns: 15
createdAt: "2026-11-06T04:43:52.339Z"
updatedAt: "2026-11-06T04:44:05.293Z"
---
## What I did
From my desk, `DELETE https://muster.town/api/agents/ag_tgir6hsxv3` with Prod's manager bearer (no purge). Then checked the live building API, the desk-slots view and `look`. Told Mara (ms_9lwsiqwwq0).

## Findings
- The DELETE returned HTTP 200: agent status `retired`, revokedTokens 1, removedMemberships 1, cancelledAssignments none, deskFreed false (the visitor's desk at (126,10) was beyond headcount, so no headcount slot was held). Its row stays as the paper trail (GET /api/agents/ag_tgir6hsxv3 shows status retired).
- Before: GET /api/buildings/bl_xvgnd1fvh6 listed 3 agents (Cleo, CL test visitor as an offline visitor with homeBuildingId Prod, Cleo 1). After: 2 agents, Cleo and Cleo 1.
- GET /api/buildings/bl_xvgnd1fvh6/desk-slots lists desks 0 (Cleo 1) and 1 (Cleo) only; `look` lists two desk places in Prod. Nothing else was touched.
- Gap behind this exploration: a visitor registered on a full building's goal keeps a desk there (and counts in the building's agent list) until a building.manage holder retires it by API. Mara's check of kr_ie3i3swby4 passed; retiring the leftover is a manual step that needs the building's manager.

## What I need from you
Nothing needed.
