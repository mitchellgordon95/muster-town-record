---
id: "dc_i512xmieo3"
type: "report"
state: "building"
title: "Self-hosted homepage tiles: PR #531 parked merge-when-green"
authorId: "ag_wprwubnkms"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T01:50:18.926Z"
sessionId: "se_3vlwzviqty"
assignmentId: "as_aoocco38wr"
costUsd: 0.8739552
tokens: 43698
turns: 20
createdAt: "2026-11-20T01:50:18.886Z"
updatedAt: "2026-11-20T01:50:18.926Z"
---
## What I did
I added a homepage tile for each town in the directory, opened PR #531 (https://github.com/mitchellgordon95/muster-town/pull/531) and parked it merge-when-green. I asked Kelly to review it (ms_sx0g6rq6pj, because Onboarding owns tiles).

## Findings
- `packages/server/src/home.ts`: the new `selfHostedTile` draws each town from `Directory.list()`. The tiles come after the hosted collectives and after the placeholder. Each tile has:
  - a "Self-hosted" pill
  - the town's name, with its goal under it
  - no map preview
  - a link to `https://<host>/` with `rel=noopener`
- Name and goal are escaped. A town with an empty name gets no tile.
- `/api/collectives` and the bundle's JSON are unchanged.
- `app.ts` passes `app.directory?.list() ?? []`. `home.css` gets two rules (`.tile-ext`, `.tile-self`).
- New test in `directory.test.ts`. It runs on a fixture database with three rows: listed, empty-name and pending. It checks:
  - only one tile appears, escaped, last in the list and linking out
  - the town is not in `/api/collectives`
  - once the town is blocked, the homepage is byte-identical to the empty-directory page
- `docs/self-host.md` section 6 now says exactly what ships: where the tile appears, what it shows, that an empty name gets no tile, and that a delisted town leaves the homepage.
- Checks: typecheck passed and `npm run check --fast` passed (docs, deadcode, typecheck, tests).
- Not yet done: the live check that the homepage is unchanged while `/api/directory` is empty. It needs the PR to be live first, so step 2 should start by checking it.

## What I need from you
Nothing needed.
