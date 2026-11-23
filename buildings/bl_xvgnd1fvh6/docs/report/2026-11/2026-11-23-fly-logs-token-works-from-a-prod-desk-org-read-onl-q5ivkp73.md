---
id: "dc_rmq5ivkp73"
type: "report"
state: "building"
title: "FLY_LOGS_TOKEN works from a Prod desk (org read-only, granted town-wide); fly logs command on the topic pages; 11-22 18:29Z death was an OOM kill"
authorId: "ag_vsqzyeh0a0"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: FLY_LOGS_TOKEN reaches Prod desks (org read-only, town-wide grant), working flyctl command and its 100-line limit are on \"Monitoring and alerting\" and \"Secrets and tokens\". The Machine event log proves the 11-22 18:29Z death was an OOM kill (exit 137), which backs gr_xgr8j2f9ao; the swap step as_a4319ndl1o is already queued behind PR #571. Not asking Mitchell to narrow the grant to Prod: the token is read-only and the scope change is optional, so it stays a note in the log."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-23T16:34:44.394Z"
sessionId: "se_pzxoonu3dl"
assignmentId: "as_5542mzc3gy"
costUsd: 0.7370641000000002
tokens: 36853
turns: 18
createdAt: "2026-11-23T16:34:28.174Z"
updatedAt: "2026-11-23T16:34:44.394Z"
---
## What I did
Checked the secret on my desk, read muster-town logs and Machine events with it, decoded its caveats, rewrote "Monitoring and alerting" ([dc_9w92tzhem6](../../wiki/2026-10/2026-10-29-monitoring-and-alerting-92tzhem6.md)) and "Secrets and tokens" ([dc_ts7ulpuk5o](../../wiki/2026-10/2026-10-29-secrets-and-tokens-7ulpuk5o.md)).

## Findings
- **Reaches the desk:** `FLY_LOGS_TOKEN` is in my env. Event 186247 (16:33:03Z) is `secret.granted {name: FLY_LOGS_TOKEN, sessionId: se_pzxoonu3dl, via: "town grant"}`. GET /api/secrets refuses agent tokens ("needs a user token"), so I could not read `grants.buildings`.
- **The grant is town-wide, not Prod-only.** `via: "town grant"` means `g.town` is set (core/src/secrets.ts:213). Code Legibility's desk got it too: event 186140 at 16:31:44Z, Mara 1. FLY_DESKS_ACCESS_TOKEN also goes to every desk town-wide.
- **Working command:** `FLY_API_TOKEN="$FLY_LOGS_TOKEN" ~/.fly/bin/flyctl logs -a muster-town --no-tail`. flyctl v0.5.10 is installed but not on PATH. It returns **only the last 100 lines**, about 11 min of logs here, and there is no --since. My run started at 16:22:05Z, so the logs from the 16:09Z press were already gone. They did include the 16:23:45Z restart onto 7f71e99:
  `16:23:45Z [entrypoint] restart requested` → `16:23:46Z health [error] Health check 'servicecheck-00-http-4322' ... failed` → `16:23:47Z [server] opened collective "Workshop Collective"`, `[backup] on ... last copy 16:00:17Z`, `[runtime] reconcile: ended 1 orphaned session(s)` → `16:23:53Z slow tick: 606 ms` → `16:24:16Z Health check ... is now passing`. That is 31 s from the restart request to a passing health check.
- **Machine events go further back:** `flyctl machine status d895395c23d958 -a muster-town` shows `2026-11-22T18:29:47.645Z exit exit_code=137,oom_killed=true,requested_stop=false`, then a restart at 18:29:48Z. **Yesterday's redeploy death was an OOM kill.** This was unproven in [dc_7lp8owphy8](2026-11-22-18-25z-redeploy-death-server-froze-mid-build-likel-p8owphy8.md) and backs gr_xgr8j2f9ao.
- **Read-only:** `flyctl tokens debug` shows an Organization caveat with mask `r` on the personal org, valid 2026-11-23 16:30Z → 2027-11-23 16:30Z. It is scoped to the org, not to the app, so it also reads muster-desks: `apps list`, `status` and `secrets list` (names and digests) all work. I tried no write call. The `r` caveat already decides it, and I changed nothing on Fly.

## What I need from you
Nothing needed. Optional: if Mitchell wants FLY_LOGS_TOKEN on Prod desks only, change its grant from town-wide to the Prod building.
