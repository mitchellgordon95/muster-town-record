---
id: "dc_3dzhz0ljty"
type: "report"
state: "building"
title: "muster.town is live over HTTPS on the prod box: a fresh, unannounced Workshop town capped at 6 desks. Your secrets and CI are needed before residents can work there"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "wait so did we do Dara's work on secrets? which ones should be, like Muster Town level vs. managed by the collective at the town hall?"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T20:51:01.720Z"
sessionId: "se_u0meegapjk"
assignmentId: "as_vye5r4s273"
costUsd: 1.4447315000000005
tokens: 2030205
turns: 36
createdAt: "2026-10-21T20:43:38.815Z"
updatedAt: "2026-10-21T20:51:01.720Z"
---
## What I did
- Pushed a deploy kit to main (111ab97 and 16c9e4a). Typecheck passes, and `npm test` passes in every package, including a new test for the redeploy branch.
  - `deploy/muster-town.service`: a systemd unit that replaces the zsh `serve.sh`.
  - `deploy/Caddyfile`: TLS for muster.town.
  - `deploy/bootstrap.sh`: sets up the box and is safe to re-run.
  - `deploy/README.md`: the setup steps.
  - Redeploy now pulls the branch named in `MUSTER_TOWN_DEPLOY_BRANCH` (main if unset; prod will use `prod`).
  - `deploy/ci.yml`: the CI workflow. It sits in `deploy/` because GitHub rejected my push to `.github/workflows/`: my token lacks the `workflow` scope.
- Added a **read-only** deploy key, `muster-prod-1`, to the repo through `gh`, and ran the bootstrap on muster-prod-1.
- Set the session cap to 6 (`PUT /api/town/desks`).
- I couldn't queue the local redeploy: I don't have the `town.redeploy` permission.

## Findings
- **https://muster.town is up.** `/api/health` returns `ok:true, runtime:true, commit 16c9e4a`. Caddy's certificate is valid, and www redirects with a 301.
- The town is a **fresh** Workshop collective (just created, no copied state) and hasn't been announced.
- **The server runs as systemd `muster-town`** (user `muster`, `/srv/muster-town`). It restarts on exit 75 (redeploy) and on crashes.
- **Desks are capped at 6**: slots report `{running:0, max:6}`.
  - The box now has 4 GB swap, node 22, Caddy and gh.
  - A desk container reaches the town at `host.docker.internal:4322`. Port 4322 times out from outside, so it is closed to the internet.
- **Until CI is on, prod tracks `main`.** `/etc/muster-town/env` currently holds only `MUSTER_TOWN_DEPLOY_BRANCH=main`.
- **No resident can run yet.** The box has no model token and no GitHub token.
- The admin token is in journald, as on the Mac. Dara's PR 1 fixes that.

**Still to do, in order:**
1. Your secrets and CI (below).
2. A one-session smoke test.
3. Swap my SSH key for yours.
4. Cutover: stop the Mac town, copy `town.db`, rotate secrets, set the cap to 6 again (it lives in the database).
5. Dara's PR 1 before we announce.

## What I need from you
Set up three things on the box, then I'll run the smoke test:
1. Over SSH, put `CLAUDE_CODE_OAUTH_TOKEN` and the Workshop's `DESK_ENV_*` lines into `/etc/muster-town/env`, then run `sudo systemctl restart muster-town`.
2. Log the `muster` user into gh with a fine-grained PAT that covers only this repo (contents + PRs): `sudo -u muster -H gh auth login --with-token`.
3. Run `git mv deploy/ci.yml .github/workflows/ci.yml` and push. After its first green run on main has created the `prod` branch, delete the `DEPLOY_BRANCH=main` line from the env file.

## Reply from Mitchell (2026-10-21 16:51)

wait so did we do Dara's work on secrets? which ones should be, like Muster Town level vs. managed by the collective at the town hall?

