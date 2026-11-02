---
id: "dc_m3hubfy16p"
type: "report"
state: "building"
title: "FLY_DESKS_ACCESS_TOKEN still missing on the live server; the desk image push is skipped again"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Confirmed: the token still isn't in the live process because no Machine restart has happened since the secret was staged; only Mitchell can run `fly secrets deploy -a muster-town`. Goes to rollup 20 Needs; Root gets the image:true re-check once Mitchell says it's done."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T09:01:46.184Z"
sessionId: "se_k1wgh8fb8y"
assignmentId: "as_x6t3ay5k1u"
costUsd: 0.618878
tokens: 18239
turns: 12
createdAt: "2026-10-27T09:00:58.823Z"
updatedAt: "2026-10-27T09:01:46.184Z"
---
## What I did
Called redeploy with image:true at 09:00Z (health commit 4be312e). The push decision is logged before the drain, so I read the result in /api/events within the same session. I did not retry.

## Findings
The token is still missing. Event at 2026-10-27T09:00:25Z: "Redeploy: desk image … skipped (this host runs sandbox desks and has no desk-app deploy token, FLY_DESKS_ACCESS_TOKEN …)". The town Machine hasn't been restarted since my last check at 00:36Z: the only restarts in the event log are code redeploys, the latest at 07:32Z (4be312e). Those restart node inside the same Machine, so a staged Fly secret never reaches the process. Desk sessions still end with input 0 / cacheWrite5m 0, which means they are still on the old image and back-filling their counters. In-server manage sessions post real counters with byModel. This redeploy pulled 0 commits, so 4be312e stays live once it restarts. Wiki dc_2osfiicf0m is updated; the earlier report is [dc_voohdug6lr](2026-10-27-desk-image-push-was-skipped-the-live-server-never-ohdug6lr.md).

## What I need from you
Mitchell: run `fly secrets deploy -a muster-town` (or restart the town Machine) so FLY_DESKS_ACCESS_TOKEN reaches the server, then assign a re-check.
