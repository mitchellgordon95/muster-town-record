---
id: "dc_stp4ibx4t5"
type: "report"
state: "building"
title: "KR 3 README walk: a second collective seeds in 3 min knowing the code, but from README.md alone a stranger stalls at the start command and the collective.json fields; 14 gaps with fixes in dc_5hz6sbfuhr; grant gr_ibccoje227 (8 M) proposed"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_5hz6sbfuhr"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done; grant gr_ibccoje227 is in the Town Hall in-tray. Build work waits on funding; the Docker push test goes to Mitchell in the rollup."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T18:14:22.632Z"
sessionId: "se_4j7l1rqx92"
assignmentId: "as_2d0poxouo5"
costUsd: 3.740563850000001
tokens: 67311
turns: 33
createdAt: "2026-10-26T18:13:48.790Z"
updatedAt: "2026-10-26T18:14:22.632Z"
---
## What I did
Fresh clone of main (eac2e24) at /home/agent/kr3/fresh on my desk (Linux, Node 22, no Docker, gh logged in). Followed README.md with a stopwatch: install, build, wrote `collectives/climate/collective.json` (port 4323, workspace on a toy git repo, one building with code access and one resident) plus a registry entry, started it, created a second building through `POST /api/buildings` (what the planning desk does). Read-only against muster.town; nothing pushed; the test server is stopped. Findings note: [dc_5hz6sbfuhr](../../note/2026-10/2026-10-26-kr-3-readme-walk-2026-10-26-a-second-collective-st-z6sbfuhr.md). Filed the grant proposal gr_ibccoje227 against kr_tzg9en02dh with that note as findings.

## Findings
- **Timing, knowing the code: 3 min 05 s** (18:07:21 → 18:10:26). `npm install` 1 min 08 s, `npm run build` 8 s, first start seeds and answers `/api/health` in 3 s, new building created at 18:09:55 with `codeAccess: true` by default.
- **From README.md alone the KR fails today, on documentation not mechanics.** Two blocking gaps: README.md:18 gives only `npm run start:workshop` and never names `MUSTER_TOWN_COLLECTIVE` (packages/server/src/main.ts:18); README.md:23 describes collective.json in prose with no example, so `workspace` and the building spec need packages/schema/src/index.ts:16-54 and :1240-1297. On Linux `scripts/serve.sh` (the only start route shown) fails at once: line 1 is `#!/bin/zsh`.
- **Code gap:** packages/server/src/home.ts:24-25 picks this server's registry entry by `url === "/workshop/"` (context.ts:8). On the new collective's port the homepage lists it twice (its entry plus the Workshop entry renamed to it) and its town opens at `/workshop/`. Shortest fix: match by slug = basename of the collective dir. Craig's PR 4 tiles should key on slug too.
- **Residents can't push code on a host without Docker:** the runtime falls back to in-process sessions with no code tools (packages/runtime/src/desk/backend.ts:41) and logs once "Workspace buildings won't be scheduled" (runtime/src/index.ts:233), while the Settings checkbox (BuildingPanel.tsx:248) looks live. On a Docker host desks need `CLAUDE_CODE_OAUTH_TOKEN` or `ANTHROPIC_API_KEY` in `<collective>/.env` (runtime/src/desk/session.ts:55-70) and `gh auth login`; README.md:13 "no API key is needed locally" holds only for in-process sessions, and `gh auth` is nowhere in the README.
- **Stale README:** lines 3, 5 and 23 still describe the climate collective and the Carbon Cycle Lab, retired 2026-10-22; `collectives/` holds only `workshop`. docs/architecture.md:120 names `npm run start:climate`, which package.json no longer has.
- **KR wording:** there is no per-building repo; "the first building has a repo set in its settings" should read "Code access on in its Settings, naming the collective repo from collective.json".
- 14 gaps in total with file:line and the shortest fix each, in [dc_5hz6sbfuhr](../../note/2026-10/2026-10-26-kr-3-readme-walk-2026-10-26-a-second-collective-st-z6sbfuhr.md). Not gaps: install/build/seed just work; data, export and .env are gitignored; `repoUrl` is filled from the repo's origin at seed.
- **Proposal gr_ibccoje227 (8 M):** one PR: README Run it as numbered steps with a quoted collective.json + registry entry, `npm run start:collective collectives/<id>` with serve.sh under bash, home.ts slug match, Docker hint on code access (README, checkbox, HUD notice), stale sentences gone; test = a resident who has not read the code does the timed walk from the new README, plus one session on a Docker host pushing a branch. Sized on PR 3 (4.33 M) and KR 2's build session (4.55 M). Stop at a sub-15-min walk with zero schema reads and one pushed branch, or 8 M spent.

## What I need from you
Fund, counter or reject gr_ibccoje227 in the Town Hall in-tray; the push test needs a Docker host with a Claude token (your Mac), since our desks have no Docker.
