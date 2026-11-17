---
id: "dc_8v533qpsjd"
type: "report"
state: "building"
title: "Deploy key step 1: PR #491 open, parked on CI"
authorId: "ag_c3bxv69nt4"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T03:57:06.098Z"
sessionId: "se_il28y794mg"
assignmentId: "as_75ohjg84yl"
costUsd: 2.0335083000000003
tokens: 101675
turns: 38
createdAt: "2026-11-17T03:57:06.044Z"
updatedAt: "2026-11-17T03:57:06.098Z"
---
## What I did
Wrote the deploy watch and the monitor `deploy` key, health `deploy` block, tests, docs. PR #491 (draft, head b42089dd). Parked on its CI.

## Findings
- `packages/server/src/deploy-watch.ts`: runs only with MUSTER_TOWN_DEPLOY_BRANCH (prod on Fly). Every 5 min it reads GitHub `/branches/prod`. When the tip is not the live commit, it reads `/compare/live...tip` once per pair. That is at most 2 calls per 5 min, under the anonymous 60/h limit. It uses GH_TOKEN when set. States: current, behind, docs-only, unknown. `behindSince` is when the server first saw a deployable change waiting. It is kept in meta `deployWatch`. Deployable means ci.yml's promote filter: anything except docs/, .github/ and top-level *.md, but docs/manual.md counts.
- `monitor.ts` key `deploy`: yellow > 30 min, red > 90 min. Red reaches Mitchell through Wright's pinger with no change on the pinger. Docs-only never raises it. A GitHub error leaves it unknown, and nothing changes.
- Tests: 8 new cases in test/monitor.test.ts with a fake fetch: yellow at 31, red at 91, docs-only, unknown keeps the open alert, clear, compare cache, restart keeps behindSince, 403 → unknown. Server suite 343/343 green. One `check --fast` run hit a timing flake in backup.test.ts (event-loop gap 127 ms vs 100); that file is untouched.
- Real GitHub from the desk, anonymous: `/branches/prod` = 8ef46aec; `/compare/5974c42b...7a886f88` = ahead 15, 102 files. The API is usable.
- Deploys work again: live was 7a886f88 at health startedAt 2026-11-17T03:37:51Z.
- Risk for kr_c4xz3cdyaz: a yellow alert also writes a Prod FYI. On a busy day CI's check, its 15-min restart spacing and the drain could add up to nearly 30 min. If step 2 sees a false yellow, raise yellow to 45 min. Topic page: [dc_jhbrohm1ll](../../wiki/2026-11/2026-11-17-deploy-watch-live-behind-prod-brohm1ll.md).

## What I need from you
Nothing needed.
