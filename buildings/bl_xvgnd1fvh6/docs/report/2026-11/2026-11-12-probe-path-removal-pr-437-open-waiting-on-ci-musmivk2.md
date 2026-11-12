---
id: "dc_hcmusmivk2"
type: "report"
state: "building"
title: "Probe path removal: PR #437 open, waiting on CI"
authorId: "ag_d56a3tz8g3"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The continuation is already parked on PR #437's CI (as_sjfn4288t9); nothing else to queue. Migration 113 is additive (deletes the prober role row), so no data-loss call."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-12T16:43:37.749Z"
sessionId: "se_qut281d9kc"
assignmentId: "as_qeyqnqgtgn"
costUsd: 1.0645901
tokens: 53230
turns: 19
createdAt: "2026-11-12T16:43:29.777Z"
updatedAt: "2026-11-12T16:43:37.749Z"
---
## What I did
Opened draft PR #437 (https://github.com/mitchellgordon95/muster-town/pull/437). It removes the probe POST, the prober role, town.uptime and the Pinger's posting. Parked until its CI finishes.

## Findings
- Removed: `POST /api/uptime/probes`, `Uptime.ingest` and `ProbeBatch`, the `town.uptime` permission, and built-in role `prober` (schema plus migrate-roles). Migration 113 deletes the `role:prober` row and any membership in it. It is additive, and 112 is the highest number on main right now.
- Kept: table `uptime_probes` and `GET /api/uptime`. Until step 2 the route returns empty minutes plus restart gaps.
- The pinger now only alerts. Its buffer, `MUSTER_PINGER_TOKEN` and the posting code are gone, and its tests were rewritten for the alert path (2 pass).
- Text changes: the landing page, the home fallback and the Uptime block now say "Measured by UptimeRobot". deploy/README and docs/architecture.md are updated, and the log entry is in docs/log.d.
- Checks so far: typecheck passes. These suites pass: core vitest (935), server uptime.test.ts (6), web uptime.test.tsx (2) and the pinger unittest. The full server suite was left to CI.

## What I need from you
Nothing needed.
