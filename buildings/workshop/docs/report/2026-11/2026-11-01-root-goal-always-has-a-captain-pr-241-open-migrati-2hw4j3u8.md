---
id: "dc_zd2hw4j3u8"
type: "report"
state: "building"
title: "Root goal always has a captain: PR #241 open (migration 078), waiting on CI"
authorId: "ag_dsvsu5nj62"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #241 (root always has a captain, migration 078) built from main, local checks green; continuation as_t6sjfn2039 waits on {pr: 241} and carries merge (recheck migration number), redeploy and the live check (root owner = Mitchell, in-tray Mine). Rollup 37 candidate once live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T01:59:44.967Z"
sessionId: "se_p939ypcb9o"
assignmentId: "as_mnahvr6rn8"
costUsd: 2.1146556
tokens: 105733
turns: 47
createdAt: "2026-11-01T01:59:37.699Z"
updatedAt: "2026-11-01T01:59:44.968Z"
---
## What I did
I built 1:1 mt_cyd2t5ioob decision 7 as one PR from main: **PR #241** (https://github.com/mitchellgordon95/muster-town/pull/241). Typecheck, docs and deadcode checks pass. Core, server and web tests pass, apart from one backup.test timing flake (102 ms against a 100 ms limit) that passes when run again. The work is parked until CI finishes.

## Findings
- **Live right now (d9f28c5, read 01:59:18Z):** `GET /api/goals` shows the root's `ownerId` as null and its owner as "the town admins". So the earlier canvas work did not set a root captain, and the migration will fill it in rather than collide with anything.
- **Migration 078** (077 is taken by #238): it sets the `gl_town` captain to the first admin. That is the earliest admin with a GitHub account (Mitchell on muster.town), or the earliest admin if none has one. A root that already has a captain is left alone.
- **Boot and seeding:** `Goals.ensureRootCaptain()` runs at boot (`ensure()`), after seeding, when an allowlisted admin signs in with GitHub, and in `hub.open` after a hosted founder is made admin. On a hosted collective the seeded placeholder admin has no GitHub account, so the founder takes over the root. The root's captain can be changed but not cleared.
- **"The town admins" fallback removed everywhere:** `ownerOf` and `route` now always return a user id. Changed: in-tray routes (Mine shows only what routes to the viewer), captain requests (asking for the root is allowed and goes to the root's captain), the review deck, the desk brief, `GET /api/goals/:id`, the schema types, the web Captain form (no "The town admins" option at the root), the mock, and docs/goals.md "Captains on nodes" and "Routing".
- **Admin-only branches that remain (permission, not routing):** `canFund` through `building.fund`, `canEdit` through `goals.edit`, `canDecideCaptain` through `canEdit`. One more: the in-tray still opens on All for admins, and only non-admin captains start on Mine.
- **New tests:** a root with no captain is repaired at boot; a founder takes over from the placeholder admin; a captain request for the root routes to the root's captain; an admin who captains nothing has an empty Mine; clearing the root's captain is refused.
- **Next session:** merge if CI is green (check main's highest migration number first), redeploy, then check live that the root's owner is Mitchell and that Mitchell's in-tray Mine shows the items routed to the root. Then add the Shipped candidate to [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md). Topic page: [dc_roeig7abhg](../../wiki/2026-11/2026-11-01-root-goal-always-has-a-captain-mt-cyd2t5ioob-d7-eig7abhg.md).

## What I need from you
Nothing needed.
