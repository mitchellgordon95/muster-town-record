---
id: "dc_9dweiz7i0f"
type: "report"
state: "building"
title: "PR #448: CI image deploy step, parked on its CI"
authorId: "ag_ioxxmcqen3"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked continuation as_ns1oprjvfj merges #448 on green; the secret FLY_TOWN_DEPLOY_TOKEN is already asked of Mitchell in ak_yhxjzh3m7x. Nothing more to file."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-13T23:48:07.731Z"
sessionId: "se_nh1dn0d3c3"
assignmentId: "as_s7fwpkkyge"
costUsd: 1.2715537999999995
tokens: 63578
turns: 20
createdAt: "2026-11-13T23:27:16.869Z"
updatedAt: "2026-11-13T23:48:07.731Z"
---
## What I did
Added a gated `fly deploy` step to ci.yml's image job and updated deploy/README.md, the fly.town.toml and build.sh headers, plus a docs/log.d entry. Opened draft PR #448 (https://github.com/mitchellgordon95/muster-town/pull/448). `npm run check --fast` passed on the desk on the second run (the first run failed at tests). I am parked on its CI and will merge it when it is green.

## Findings
- **The ghcr image is public.** An anonymous token from ghcr.io/token followed by a manifest GET for `muster-town:prod` returned 200. That means Fly can pull `ghcr.io/mitchellgordon95/muster-town:<sha>` without logging in, so the step uses `flyctl deploy --image` and does not need the ctx-build fallback.
- **When the step deploys:**
  - It runs only on pushes to main.
  - Without the `FLY_TOWN_DEPLOY_TOKEN` secret it exits 0 and logs "not set; skipping image deploy".
  - With the secret, it reads the Machine's image from `flyctl machine list --json` (`.config.image`; a digest suffix is stripped).
  - If that image's tag is a main sha and none of `deploy/fly/Dockerfile`, `deploy/fly/entrypoint.sh` or `fly.town.toml` changed since then, it does not deploy.
  - In every other case it deploys. That includes today's Fly-registry image from build.sh, so the first run after the secret exists will deploy once.
  - Before deploying it waits until the server has been up 15 min, as promote does. I raised the image job's timeout from 30 to 50 min to allow for that wait.
- **What is left out of the gate:** the lockfiles and start-server.sh. From reading Dockerfile:4-5 and entrypoint.sh, the image is only the first-boot seed, and promote's redeploy (git pull + npm install on /data/repo) already refreshes those files. Promote is unchanged. So a run that deploys the image can restart the town twice, at least 15 min apart.
- **Not yet checked:** I couldn't confirm that `.config.image` keeps the `:sha` tag; flyctl isn't on the desk. If Fly rewrites it, every main run would deploy. The first gated run's summary line will show which case it is.
- **What a human checks once the secret is set:** the image job summary line on the run page ("image deploy: ..."), the image tag in `flyctl machine list -a muster-town`, and `/api/health` startedAt after the first deploy.
- Also fixed promote's stale comments that said "a push cancels this run".

## What I need from you
Mitchell: add the GitHub Actions secret FLY_TOWN_DEPLOY_TOKEN (ak_yhxjzh3m7x). Until it exists, the step only skips.
