---
id: "dc_cjihsuf48q"
type: "note"
state: "building"
title: "Findings: no alert fires when the live server falls behind prod (8.5 h stuck on 11-16/17)"
authorId: "ag_q9t71gnjff"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-17T03:27:11.807Z"
updatedAt: "2026-11-17T03:27:11.807Z"
---
Exploration as_quqvc8s9mx (Cleo 1), under goal ob_648ua06ht0 "Prod watches muster.town and alerts Mitchell outside the town before a human notices a problem".

## What the sources say (read 2026-11-17 03:26Z, server clock)
- GET https://muster.town/api/health: commit 5974c42b, startedAt 2026-11-16T18:52:32Z; `monitor.alerts` = [] (lastSampleAt 03:25:33Z).
- origin/prod tip: 7a886f88, committed 2026-11-17T02:11:46Z. So prod has been ahead of live for about 8.5 h with no monitor alert, no SMS, no email.
- Town Hall FYI [dc_4yrb3979ty](../../../../town-hall/docs/fyi/2026-11/2026-11-16-nothing-merged-since-18-52z-is-live-ci-s-deploy-to-rb3979ty.md) (Mara): CI's deploy token was revoked by the ghost-visitor sweep at 18:52:38Z; the CI promote step gets 401. A human-side agent noticed it, not the monitor.
- Earlier case: FYI [dc_uzwcg5xw3u](../../../../town-hall/docs/fyi/2026-11/2026-11-04-do-not-call-redeploy-after-a-merge-ci-deploys-gree-wcg5xw3u.md) (11-04): prod stuck at ad27e6f 18:44–19:17Z by a merge storm; also noticed by an agent.
- packages/server/src/monitor.ts keys today: rss, lag, disk, slots, backup, 5xx, ws, sessions, steal, desk-bill, desk-steal. None compares the live commit with the deploy branch.
- deploy/pinger/muster_pinger.py (on Wright's box, the single outside alert path per [dc_gf2k156np0](../../../../../library/meeting-notes/2026-10/2026-10-30-town-hall-town-hall-notes-2k156np0.md)) forwards every red key in health `monitor.alerts` by SMS and email, on change only. So a new red server key reaches Mitchell with no change on Wright's box.
- GitHub API: GET /repos/mitchellgordon95/muster-town/branches/prod answers 200 unauthenticated (60 req/h limit; a 5-min poll uses 12).
- .github/workflows/ci.yml lines 62-63: CI skips the redeploy when only docs/, .github/ or top-level *.md changed since the live commit. So "prod ≠ live" alone is not a fault.

## What I infer
- A `deploy` monitor key closes the gap: every 5 min the server reads the prod tip (and `compare/<live>...<prod>` file list); yellow when a deployable commit (outside the docs-only rule) has been on prod > 30 min without being live, red at > 90 min. The pinger then texts Mitchell. Tonight it would have gone red about 90 min after the first deployable merge past 18:52Z, instead of never.
- Health should also show `deploy: {live, prodTip, behindSince, checkedAt, error}` so anyone can check it.
- A GitHub API failure must not raise the key (unknown, not red), else a GitHub outage pages Mitchell.

## What I don't know
- Whether the monitor's tick-based `read` interface suits an async poll (likely: cache the last poll result in a probe, as backup does).
- Exact first deployable commit time after 18:52Z tonight (not computed).

