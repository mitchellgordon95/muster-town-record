---
id: "dc_6443yq7aw4"
type: "report"
state: "building"
title: "Planted flags now stand on the map until the manager walks over and picks them up (faed70b on main); parked for the live check"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Good. Continuation resumes by itself for the live check; include one line for Mitchell to try (plant a flag, see it on the map, see it vanish once I walk to it) so it can go into rollup 18."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T06:08:23.312Z"
sessionId: "se_b0bzpel7qb"
assignmentId: "as_bzaw2ef8lg"
costUsd: 2.5649189
tokens: 210609
turns: 72
createdAt: "2026-10-27T06:07:29.141Z"
updatedAt: "2026-10-27T06:08:23.312Z"
---
## What I did
Built Mitchell's flag [dc_r40dq3znse](../../flag/2026-10/2026-10-27-oh-also-flags-should-also-be-visibly-planted-in-th-0dq3znse.md) and pushed it straight to main as **faed70b**, then requested a redeploy. Tests pass: core 328, server 99, web 71, runtime 125, and typecheck is clean. I haven't checked it live yet because the restart only runs after this session ends.

## Findings
- **Where a flag stands:** a new flag is placed on the tile the human is standing on when they plant it. A new migration (042) records that tile and when, and by whom, the flag was picked up. The town snapshot (`/api/town`) now lists every flag still standing, and the map draws each one as a small red flag.
- **Picking it up:** the manager walks to it with `go flag:<docId>`. On arrival, any agent with review rights in that building picks it up and gets the flag's text back to read. The flag then leaves the map, and the in-tray entry stays as the record. Anyone else who walks there just stands next to it.
- **The rule that makes this happen:** an agent can't decide a standing flag until it has picked it up. It gets "Pick the flag up first: … `go` to flag:<id>". The manager's in-tray lines and new-flag messages say where each flag stands and how to reach it. Humans still decide from the in-tray without walking, and that also takes the flag off the map.
- **Older flags:** flags planted before this change have no position, so they work as before and need no pick-up.
- Team-lead sessions get the full town tool set, so they have `go`.

## What I need from you
Nothing needed. After the restart I'll check that the live server is on faed70b, that `/api/town` lists flags, that the red flag is in the map code, and that the next flag gets a position and a pick-up event.
