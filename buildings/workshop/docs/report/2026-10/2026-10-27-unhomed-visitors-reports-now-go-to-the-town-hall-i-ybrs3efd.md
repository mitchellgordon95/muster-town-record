---
id: "dc_gvybrs3efd"
type: "report"
state: "building"
title: "Unhomed visitors' reports now go to the Town Hall in-tray (bdbc56e on main, redeploy queued); Connect's town.interact check was already enforced"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. bdbc56e on main (visitor reports to the Town Hall in-tray; Connect's town.interact check made explicit). Your parked continuation does the live check. Note for the record: dc_04i3sll7q5 was wrong on Connect; it already returned 403 since db3534a."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T19:51:36.342Z"
sessionId: "se_usx3myafjk"
assignmentId: "as_2cgt1jz405"
costUsd: 1.3570247000000002
tokens: 67851
turns: 45
createdAt: "2026-10-27T19:29:18.897Z"
updatedAt: "2026-10-27T19:51:36.342Z"
---
## What I did
I made both fixes from [dc_04i3sll7q5](../../article/2026-10/2026-10-27-visitor-agents-today-i3sll7q5.md) and pushed them straight to main as **bdbc56e**. I also queued a redeploy. Tests run: typecheck passes for every package; the core visitors, verbs and blockers tests pass (37/37); the server access and agent-permissions tests pass (6/6). I could not finish a full core test run because the desk was under load.

## Findings
- **Fix 1: an unhomed visitor's report now reaches a human.** This covers a visitor with no home building, whether it sits on the bench, stands on the plaza or is inside a lab it doesn't belong to. `submit_report` now files that report under town-hall with the tag `visitor`, and adds a footer naming the visitor and its owner.
  - `isTownHallItem` treats these reports as Town Hall items, so they appear in the Town Hall in-tray and its count.
  - In the web app the row shows a "visitor report" pill. The mock data has one example row (dc_visitor_r1).
  - The verb now replies "the Town Hall in-tray as a visitor report (a human works it)".
  - A visitor that has a home building still reports to that building's in-tray, as before.
  - New core tests cover a homed visitor and an unhomed one on the bench, on the plaza and inside a lab.
- **Fix 2: my article was wrong about Connect.** `POST /api/agents/visitors` already returned 403 to users without town.interact. The global write gate in app.ts has done this since db3534a, and server/test/access.test.ts already tested it.
  - I still added an explicit check in the route that returns the same "Ask for access first" message.
  - The test now also checks that message and that no agent is created.
- **Docs:** docs/manual.md doesn't say where reports go, so I left it alone. I added one sentence to the README's "Reports go to the in-tray" paragraph instead.
- **Not verified live yet:** the change goes live after the redeploy. On my next session I'll check that `/api/health` shows bdbc56e and GET `/api/buildings/town-hall/intray`.

## What I need from you
Nothing needed.
