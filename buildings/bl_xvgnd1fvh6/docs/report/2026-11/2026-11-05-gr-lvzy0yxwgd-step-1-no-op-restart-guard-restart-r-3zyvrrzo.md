---
id: "dc_3g3zyvrrzo"
type: "report"
state: "building"
title: "gr_lvzy0yxwgd step 1: no-op restart guard + restart reason + tool text in PR #365; parked on its CI"
authorId: "ag_8u1m73yo41"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 built and parked on PR #365's CI; its continuation as_wyuqkctq19 already waits on {pr:365} (merge on green, no redeploy). Nothing more to queue. The Planning-panel Redeploy button side effect is noted for the rollup, not acted on (web code, Mitchell's call)."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-05T20:11:06.143Z"
sessionId: "se_vf545zkkg0"
assignmentId: "as_oe482l2y7v"
costUsd: 1.3066276000000003
tokens: 65331
turns: 25
createdAt: "2026-11-05T20:10:59.274Z"
updatedAt: "2026-11-05T20:11:06.143Z"
---
## What I did
Built step 1 of gr_lvzy0yxwgd in one PR, tested it locally, pushed it and opened draft PR #365: https://github.com/mitchellgordon95/muster-town/pull/365. Updated the topic page [dc_2s9vd1kmgf](../../wiki/2026-11/2026-11-05-no-op-restart-guard-gr-lvzy0yxwgd-9vd1kmgf.md). I am parked until the PR's CI finishes; on green I merge it and do not call redeploy.

## Findings
- **The guard** (packages/runtime/src/redeploy.ts, new step a2 right after the first pull): it fires when `world.host.commit` (the commit /api/health reports) is known, the request has no image and no `restart`, and HEAD after the pull equals that live commit. The run then ends with one terminal event: "Redeploy: nothing new on <branch> (live <sha7>); no restart. CI deploys a merge once main is green. Give restart: "<reason>" for a deliberate restart." The event carries payload `noop: true` and run state `done`, commits 0. There is no build, no drain and no exit 75. The monitor's `redeploy-failed` metric reads `done` as clean.
- **Paths that still restart:** a pull that brings commits, a checkout already ahead of the running server, an unknown live commit (dev checkout), image=true, and a `restart` reason. A request that joins the run with a reason or image is honoured: the guard re-reads them after its await, and the again/done-file carry the reason. CI's promote job is unaffected, because it moves `prod` first, so its pull always brings commits.
- **`restart?: string`** (trimmed, 1–500 characters) is added to the MCP `redeploy` verb, `RedeployInput` (POST /api/admin/redeploy), `HostHooks.redeploy` and `RedeployRequest`. The "Redeploy requested by X (restart: <reason>)" event names the reason.
- **Tool text** rewritten: CI fast-forwards `prod` and redeploys every green main, so don't call redeploy after a merge. Use it for image=true or `restart: "<why>"`. A call with nothing new ends without restarting. The lines about never polling and parking on {deploy: sha} are kept.
- **Tests:** 7 new tests under "no-op guard" in packages/runtime/test/redeploy.test.ts cover: no-op, reason, joining reason, image, new commits, checkout ahead of live, and unknown commit. One existing call-order test gained a `git rev-parse HEAD` line, because the test runtime's host.commit is the real checkout HEAD. Results: runtime redeploy 33/33, server redeploy 4/4, `npm run typecheck` clean, knip clean.
- **Side effect:** the web Planning panel's Redeploy button sends no reason, so a human who presses it with nothing new now gets the "nothing new" event instead of a restart. That is web code and I left it alone. A reason field there would be a small follow-up if Mitchell wants a restart button.

## What I need from you
Nothing needed.
