---
id: "dc_ihwq7bfi4o"
type: "flag"
state: "building"
title: "for some reason i see a bunch of managers lingering around the town hall meeting desk. some are working and some are no…"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_ihwq7bfi4o (2026-10-29 ~20:55Z, planted at (55,33) by the town hall meeting desk): \"i see a bunch of managers lingering around the town hall meeting desk. some are working and some are not. i think we generally want residents to hang out at their desks, except when they're doing meetings or talking to other residents?\"\n\nMake that the rule in code. (1) Diagnose first: look at the live town (GET /api/town or /api/agents positions) and the event log to see which agents are standing at the Town Hall meeting room right now and why they stayed: most likely bodies are left wherever the last `go` put them when a meeting ends or a session ends, and nothing walks them home; also check what happens to a manager's body when a meeting ends or a fork retires. Name the code paths (core meetings end handler, session end, idle agents, `go`). (2) Implement: when an agent is not in a meeting (or walking to one) and is not talking to someone (recent `say`, or a `go` to another agent), its body goes back to its own desk: at the latest when a meeting it attended ends and when its session ends. Walking is free, so a deterministic \"walk home\" on meeting end and on session end is fine; idle agents with no desk (visitors) keep today's behaviour. Keep it small: no schema change, no Bank change, no other building's code. Add tests. (3) PR, CI green, merge to main, queue a redeploy (plain), park the live check on your commit: after the deploy, confirm nobody idle is standing at the Town Hall meeting room, with one cropped screenshot of the map (≤300 px tall) for the rollup. Rewrite the relevant topic page (meetings dc_8qwqtmh7i5 or forks dc_3d2ssrg5ae). Report in the three-section format; verdict stop when live-checked. Do not tell Mitchell directly; it goes in rollup 31."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T20:29:24.963Z"
flagPos: {"x":55,"y":33}
pickedUpAt: "2026-10-29T20:28:58.994Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-10-29T20:28:36.746Z"
updatedAt: "2026-10-29T20:29:24.963Z"
---
for some reason i see a bunch of managers lingering around the town hall meeting desk. some are working and some are not. i think we generally want residents to hang out at their desks, except when they're doing meetings or talking to other residents?
