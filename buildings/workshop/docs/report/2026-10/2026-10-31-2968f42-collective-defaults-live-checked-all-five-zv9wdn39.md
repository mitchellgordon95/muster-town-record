---
id: "dc_gqzv9wdn39"
type: "report"
state: "building"
title: "2968f42 (collective defaults) live-checked: all five checks pass, 0 console errors"
authorId: "ag_qjkkt9mji0"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "2968f42 live since 05:27:50Z and live-checked (Town Hall collective defaults form in mock, building Settings down to Name/Attached to/Desks/Manager, live Overview \"Collective defaults\" row, PUT /api/town/defaults 401 without a session, 0 console errors). Rollup 34 Shipped item for PR #158 uses mf_g36vqg5oni; the \"save the defaults once\" item stays in Needs from Mitchell."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T05:32:36.148Z"
sessionId: "se_9tjbmuhkg9"
assignmentId: "as_0mx68v5iit"
costUsd: 1.1683566000000003
tokens: 58418
turns: 33
createdAt: "2026-10-31T05:32:29.262Z"
updatedAt: "2026-10-31T05:32:36.148Z"
---
## What I did
I live-checked PR #158. GET /api/health shows commit **2968f420** running since **2026-10-31T05:27:50Z**. I checked the API with curl. I opened the live Workshop Overview and Town Hall as a guest in headless Chromium. Guests can't see Settings, so I rendered both Settings forms in the mock dev server (`VITE_MOCK=1`, admin). No code changes.

## Findings
1. **Town Hall → Settings, Collective defaults:**
   - Mock render as admin: the section shows Model, Cheap model, Daily budget / agent, Max turns / session, Code access and "Save for every building". It also has the line naming buildings a save would change ("Saving changes Carbon Cycle Lab, Workshop (they run on other values now).").
   - Live as a guest: no Settings tab, so there is no save control.
   - `PUT /api/town/defaults` without a session returns **401** "Missing or invalid bearer token." (401, not 403: it rejects the missing login before checking admin rights).
   - Crop: ![Town Hall collective defaults (mock, admin)](mf_g36vqg5oni)
2. **Workshop Settings** (mock, admin): the form fields are Name, Attached to, Desks and Manager, then the Pool and Exploration sections. None of the five default fields are there. Crop: ![Workshop Settings (mock)](mf_y5ggzc80r8)
3. **Workshop Overview** (live): exactly one read-only "Collective defaults" row reads "claude-opus-5-5 · cheap: claude-haiku-5-5 · 1.7M adj. tokens / agent / day · 120 turns · code on mitchellgordon95/agent-town". Crop: ![Workshop Overview line (live)](mf_37rnfx5pgl)
4. **GET /api/town**:
   - `town.defaults` = {claude-opus-5-5, claude-haiku-5-5, 120 turns, 1,666,667/agent/day, codeAccess true}, the values seeded from the Workshop.
   - No building changed at boot:

     | Building | Daily budget / agent | Max turns |
     |---|---|---|
     | Workshop | 1,666,667 | 120 |
     | Onboarding | 1,333,333 | 80 |
     | Prod, Bank Transparency, Code Legibility | 1,000,000 | 80 |
     | UI / UX | 350,000 | 80 |
     | Town Hall | 333,333 | 80 |

5. **Console and page errors:** 0 on the live Workshop Overview, 0 on the live Town Hall panel, and 0 on the mock Settings renders.

I updated topic page [dc_b1xrk44eu4](../../wiki/2026-10/2026-10-28-desks-desk-image-and-manager-forks-xrk44eu4.md) to say this is live-checked, and added a short recipe for live checks.

## What I need from you
Nothing needed. The labs keep their own budgets and turn limits until an admin saves the collective defaults once; that "save once" item is already headed for rollup 34.
