---
id: "dc_vaqwy8ykpz"
type: "report"
state: "building"
title: "Forks toggle added to Building → Settings → Budget mode (543df1b pushed, redeploy queued)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. 543df1b (human-only Forks toggle in Building → Settings → Budget mode) on main, redeploy queued, typecheck clean, 98 web tests green. Your parked continuation does the live check (health 543df1b, bundle has the help line); no second assignment needed. When it is live, tell me so I drop the forks paragraph from the Scheduled with Mitchell FYI dc_6bxjb0oxzf."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T18:32:40.278Z"
sessionId: "se_pxuupehcbf"
assignmentId: "as_3q116q6coa"
costUsd: 0.8430791000000002
tokens: 42154
turns: 24
createdAt: "2026-10-28T18:25:10.486Z"
updatedAt: "2026-10-28T18:32:40.278Z"
---
## What I did
Added a human-only "Forks" on/off toggle to the Budget mode section of Building → Settings. It sits between the "Exploration / day" field and the "Save budget mode" button, with the help line "Queued building work runs on forks of the manager". I pushed it straight to main as **543df1b** and queued a redeploy. Once the server restarts, health should show 543df1b.

## Findings
- **What it does:** clicking the toggle saves at once. It sends the same PATCH /api/buildings/:id {forks} as before and shows a toast like "Forks on for Town Workshop". If the save fails, the error shows as a toast.
- **Where the value comes from:** the toggle reads the current value from GET /api/buildings/:id. To do that I added `api().building(id)` to the web client, and the mock API does the same. If the GET fails, the toggle falls back to the value the map already has.
- **Who sees it:** it shows only where the Budget mode section already shows: holders of building.fund, and never in the Town Hall. I did not change the server, the route or any permissions.
- **Checks:** typecheck is clean and all web tests pass (25 files, 98 tests). The new test, `packages/web/test/forksToggle.test.tsx`, checks how the toggle renders when on, off and still loading. It also checks that flipping the flag with the PATCH is what the GET then reads back.
- **Not yet checked:** I haven't seen the change live, and I haven't seen the toggle in a browser (my desk has none). Next session I'll check that health shows 543df1b and that the live bundle contains the help line.

## What I need from you
Nothing needed.
