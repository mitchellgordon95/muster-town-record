---
id: "dc_9w5p7793c4"
type: "report"
state: "building"
title: "PR #448 merged as 6f4bf8c0; first main run skipped the image deploy (no secret yet)"
authorId: "ag_sohd3306sy"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged. PR #448 is live on main and the deploy step is gated on FLY_TOWN_DEPLOY_TOKEN, which only Mitchell can add; the ask ak_yhxjzh3m7x already carries that, so no new ask. When his decision comes back on this thread, I will queue one check of the first gated main run (summary line, machine image tag, health startedAt, and whether Fly keeps the :sha tag)."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-14T00:04:55.543Z"
sessionId: "se_uak7pnt9id"
assignmentId: "as_ns1oprjvfj"
costUsd: 0.45053479999999996
tokens: 22527
turns: 14
createdAt: "2026-11-14T00:02:43.653Z"
updatedAt: "2026-11-14T00:04:55.543Z"
---
## What I did
PR #448's CI was green (check and image passed, promote skipped). I marked it ready and merged it at 2026-11-13 23:49:00Z as **6f4bf8c0c6e80de98ab892ca6c469ab8feb006f4**. Then I watched the first main run, 43529892211. I made no redeploy call.

## Findings
- **Every job in run 43529892211 passed:** check finished at 23:51:48Z, image at 23:54:32Z and promote at 00:02:23Z.
- **The deploy step skipped, as expected.** In the image job, the step "deploy the image to muster.town" logged `FLY_TOWN_DEPLOY_TOKEN not set; skipping image deploy` at 23:54:30Z and exited 0. So the secret did not exist at the first main run. The run page's job summary shows the same line.
- **No restart from this run.** /api/health still shows commit 5a7e229 with startedAt 23:47:21Z. Promote moved `prod` without restarting, which is fine because this change has no server code.
- **What a human checks once Mitchell adds the secret:** the next main run's image job summary should read `image deploy: ...` and should deploy once, because the Machine still runs build.sh's Fly-registry image. After that, `flyctl machine list -a muster-town` should show the image tag `ghcr.io/mitchellgordon95/muster-town:<sha>`, and /api/health startedAt should move.
- **Still unconfirmed:** whether Fly keeps the `:sha` tag in `.config.image`. If it doesn't, every main run will deploy. The first gated run's summary line will show which.

## What I need from you
Mitchell: add the GitHub Actions secret FLY_TOWN_DEPLOY_TOKEN (ak_yhxjzh3m7x). That is the only thing left.
