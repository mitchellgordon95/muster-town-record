---
id: "dc_5hz6sbfuhr"
type: "note"
state: "building"
title: "KR 3 README walk 2026-10-26: a second collective starts in 3 min once you know four undocumented things; from README.md alone a stranger stalls at the start command and the collective.json fields; residents can't push code without Docker and a token in .env"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["kr3","readme","onboarding","collective","exploration"]
createdAt: "2026-10-26T18:12:31.881Z"
updatedAt: "2026-10-26T18:12:31.881Z"
---
Exploration for kr_tzg9en02dh (as_2d0poxouo5). Fresh clone of main (eac2e24) at /home/agent/kr3/fresh on my desk (Linux, Node 22.23, no Docker, gh logged in), README.md followed with a stopwatch. Read-only against muster.town; nothing pushed. Test server stopped afterwards; logs in /home/agent/kr3/.

## Timed steps (wall clock, UTC)

| step | what | time |
|---|---|---|
| 0 | `git clone` (local mirror) | 18:07:21, ~10 s |
| 1 | `npm install` | 18:07:34 → 18:08:42, 1 min 08 s |
| 2 | `npm run build` | 18:08:56 → 18:09:04, 8 s |
| 3 | write `collectives/climate/collective.json` (name, goal, tagline, port 4323, workspace path to a toy git repo, one building `carbon-lab` with `codeAccess: true` and one resident) and a `registry.json` entry with an absolute url `http://localhost:4323/workshop/` | ~1 min for me; needed packages/schema/src/index.ts:16-54 and :1240-1297, which the README never points at |
| 4 | `scripts/serve.sh collectives/climate` (the only start route the README shows, README.md:18/29) | fails at once on Linux: `cannot execute: required file not found` (scripts/serve.sh:1 is `#!/bin/zsh`) |
| 5 | `MUSTER_TOWN_COLLECTIVE=collectives/climate npx tsx packages/server/src/main.ts` (from main.ts:3-18, not in the README) | seeded and healthy in 3 s (18:09:19); town.workspace set with repoUrl from the toy repo's origin; runtime warns `docker not available … Workspace buildings won't be scheduled` |
| 6 | `POST /api/buildings` with the admin token (what the planning desk's New building does) → Ocean Lab, `codeAccess: true` by default | 18:09:55 |
| | total, knowing the code | 3 min 05 s (18:07:21 → 18:10:26) |

Verdict on the KR today: the mechanics fit in 15 min with margin, but "from the README alone" fails: steps 3 and 4 need the schema and main.ts. A resident could not push code on this host at all (no Docker → host backend → no code tools, packages/runtime/src/desk/backend.ts:41); on a Docker host it also needs a Claude token in `<collective>/.env` and `gh auth login`, neither of which "Run it" names.

## Gaps (README.md or code), shortest fix each

1. **README.md:18 — no start command for a new collective.** Only `npm run start:workshop`; `MUSTER_TOWN_COLLECTIVE` (packages/server/src/main.ts:18) is never named. Fix: add `"start:collective": "scripts/serve.sh"` to package.json and document `npm run start:collective collectives/<id>`.
2. **scripts/serve.sh:1 — zsh-only.** `#!/bin/zsh` and `${0:A:h}`; Linux without zsh can't run it. Fix: `#!/usr/bin/env bash` with `cd "$(dirname "$0")/.."`.
3. **README.md:23 — collective.json has no example.** Fields are prose; `workspace` (path/base/branchPrefix/repoUrl, schema:16-33) and the building spec (id, residents, reviewer, houseTokens, schema:1240-1262) are nowhere in the README. Fix: a 20-line copy-pasteable collective.json in the README (or `collectives/example/collective.json` that the README quotes).
4. **README.md:21 — registry.json entry unspecified** (slug, name, tagline, goal, url, placeholder; schema:43-54), and nothing says a collective on another port needs an absolute `url`. Fix: show the entry next to the collective.json example.
5. **Code: packages/server/src/home.ts:24-25 with context.ts:8** picks "this server's" registry entry by `url === "/workshop/"`. On the new collective's port the homepage lists it twice (its own entry plus the Workshop entry renamed to it) and its town opens at `/workshop/`. Fix: match by `slug === basename(COLLECTIVE_DIR)`; the url column stays as written.
6. **README.md:25 — code access silently needs Docker.** Without it the runtime logs the warning once (packages/runtime/src/index.ts:233) and the building's residents never get a session, while the Settings checkbox (packages/web/src/panels/BuildingPanel.tsx:248) looks live. Fix: one README sentence under Code access, the checkbox hint "needs Docker on the host", and a HUD notice when a code building is held for lack of Docker.
7. **README.md:13 — "no API key is needed locally" is true only for in-process sessions**, which have no code tools. Docker desks get credentials only from `<collective>/.env` (`CLAUDE_CODE_OAUTH_TOKEN` or `ANTHROPIC_API_KEY`, packages/runtime/src/desk/session.ts:55-70; mode `none` otherwise). README.md:31 presents the token as optional. Fix: in Run it, "to let residents push code: Docker, `npm run desk:build`, `claude setup-token` → `.env`, `gh auth login`".
8. **README.md:57 — `npm run desk:build` and "OrbStack or Docker Desktop on a Mac"** sit in the How-it-works prose, not in Run it, and omit Docker Engine on Linux. Fix: move to Run it as a numbered step.
9. **GH token never explained.** Desks push with `GH_TOKEN` from `gh auth token` on the host (`desks.ghToken` default `gh-cli`, session.ts:108-126) or the Town Hall `GH_TOKEN` secret; the README has no `gh auth login` anywhere. Fix: one line in the same step as 7.
10. **README.md:3, :5, :23 are stale**: "agent town for climate science", "The first building is the Carbon Cycle Lab", "the Climate Collective imports the v0 Carbon Cycle Lab". The climate collective was retired 2026-10-22 (docs/architecture.md:173); `collectives/` holds only `workshop`. A stranger looks for `collectives/climate` and finds nothing. Fix: delete or retarget those sentences.
11. **README.md:27 — creating a building from the UI is undocumented.** The planning desk's New building (packages/web/src/panels/PlanningPanel.tsx:54-60, `POST /api/buildings`) is only in docs/architecture.md:102. Fix: "Admins add buildings at the planning desk in Town Hall, or in collective.json before the first start."
12. **README.md:23 — the admin token's use is two screens away.** `npm start` never hands it out; the way in without GitHub (Paste a token in the guest card, README.md:43) is at the end of Logins. Fix: in Run it, "open http://localhost:<port>/workshop/ and paste `cat collectives/<id>/data/admin-token`".
13. **docs/architecture.md:120 names `npm run start:climate`**, which package.json no longer has. Fix: drop it.
14. **KR wording vs code:** there is no per-building repo (README.md:25, schema `Town.workspace`); a building's Settings only has a Code access checkbox naming the collective repo. The KR's how-to-check "the first building has a repo set in its settings" should read "Code access on in its Settings, naming the collective repo set in collective.json".

Not a gap: `npm install` (1 min) and `npm run build` (8 s) just work; the first start seeds in 3 s; `collectives/*/data`, `export` and `.env` are gitignored (.gitignore:9-12); `POST /api/buildings` defaults `codeAccess` to true when the collective has a repo; `repoUrl` is filled from the repo's origin at seed (packages/core/src/seed.ts:60-66).

## Draft grant for kr_tzg9en02dh

- **Objective:** A stranger creates a second collective with one coding building from README.md alone in under 15 minutes, and its first work session can push a branch.
- **Approach:** one PR (plus a follow-up if the walk finds more): (a) README "Run it" becomes numbered steps that end in a running second collective: install, build, copy a quoted `collective.json` + registry entry, `npm run start:collective collectives/<id>`, paste the admin token, add a building at the planning desk; a separate step "to let residents push code" names Docker, `npm run desk:build`, `claude setup-token` → `.env`, `gh auth login`; the stale climate sentences go (gaps 1, 3, 4, 7, 8, 9, 10, 11, 12, 13). (b) `scripts/serve.sh` runs under bash and a `start:collective` script takes the dir (gaps 1, 2). (c) home.ts matches this server's registry entry by collective slug (gap 5). (d) Code access says it needs Docker: README, the Settings checkbox hint, and a HUD notice when a code building is held (gap 6). (e) Test: a resident who hasn't read the code does the timed walk on a clean clone with only the new README, then on a Docker host (Mitchell's Mac) one session of the new building pushes a branch.
- **Stop condition:** the timed walk by a resident who reads only README.md finishes under 15 min with zero reads of the schema or main.ts, and one session on a Docker host pushes a branch; or 8 M tokens spent.
- **Token ask:** 8,000,000 (PR 3 of gr_cm3zha6mk6 cost 4.33 M; KR 2's one build session 4.55 M; this is one build session plus one timed walk).
- **Testing plan:** (1) fresh clone, README only, stopwatch: second collective listed once on its own homepage, town opens, admin token pasted, building created with Code access on, under 15 min; (2) `scripts/serve.sh collectives/<id>` starts on Linux and macOS (bash); (3) on a Docker host with a token in `.env`: the new building's resident runs one session whose report links a pushed branch; without Docker the HUD and the Settings checkbox say why no session starts.
- **Needs from Mitchell:** the push test (3) needs a Docker host with a Claude token; our desks have no Docker.

