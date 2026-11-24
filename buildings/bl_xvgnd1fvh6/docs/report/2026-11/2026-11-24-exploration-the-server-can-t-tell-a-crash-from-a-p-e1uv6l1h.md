---
id: "dc_eqe1uv6l1h"
type: "report"
state: "building"
title: "Exploration: the server can't tell a crash from a planned restart; proposed gr_zsglqgxpew (200k)"
authorId: "ag_n4oskdbsuo"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done; its proposal gr_zsglqgxpew is rendered as a money ask for Mitchell. Nothing else to queue."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-24T00:04:17.455Z"
sessionId: "se_ctmhyqxkcl"
assignmentId: "as_rozhq4nt9s"
costUsd: 1.8935576999999997
tokens: 94678
turns: 30
createdAt: "2026-11-24T00:03:25.512Z"
updatedAt: "2026-11-24T00:04:17.455Z"
---
## What I did
I read live health and 7 days of system events (23,249 events, 11-16 18:43Z to 11-24 00:01Z). I read the boot and monitor code at ab02db89. I tested the Fly Machines API with FLY_LOGS_TOKEN from this desk. Findings are in [dc_vzsrcwcqzo](../../note/2026-11/2026-11-24-exploration-2026-11-24-the-server-can-t-tell-a-cra-srcwcqzo.md). I proposed gr_zsglqgxpew under ob_648ua06ht0. That goal had no grant before. I built on no journal line directly. This direction is new, and it follows [dc_rmq5ivkp73](2026-11-23-fly-logs-token-works-from-a-prod-desk-org-read-onl-q5ivkp73.md), the OOM find.

## Findings
- Health at 00:00:22Z showed no alerts. memAvailableMb was 1087 and swapMb 1024. restarts24h was 9. The midnight tick took 1,921 ms. dailyReset took 5.1 ms, which looks good for kr_a0mgj1zw7b; I left that claim to its own grant. Most of the tick was explore.start at 405 ms and work.forks at 813 ms.
- The server booted 52 times in 7 days:
  - 49 boots followed "Redeploy: restarting server".
  - 2 were image deploys, on 11-17 03:32Z and 11-23 17:55Z.
  - 1 was the 11-22 18:29Z OOM kill (exit 137).
- Each boot writes only "Server started" `{boot: true}`. The SIGTERM handler writes no event, and no monitor metric watches for unplanned restarts. The town never recorded the OOM kill. A desk found it a day later with flyctl.
- `GET api.machines.dev/v1/apps/muster-town/machines/<id>/events` works with the read-only FLY_LOGS_TOKEN. It returns the Machine's launch, start and exit events since its last update. The token is a collective secret, so the server can read it.
- Proposal gr_zsglqgxpew, "Alert Mitchell when the server crashes", asks for 200k in two steps:
  - Step 1 (M): record each boot's cause on the event and in health `capacity.lastBoot`. The cause comes from a stop marker plus Fly's exit code and OOM flag.
  - Step 2 (S): add a red "crash" monitor metric, so the pinger texts Mitchell, then docs and a live check.
  - Key results: kr_q82dyp154n and kr_wej5axu3iu.

## What I need from you
Fund, counter or reject gr_zsglqgxpew in the decision queue.
