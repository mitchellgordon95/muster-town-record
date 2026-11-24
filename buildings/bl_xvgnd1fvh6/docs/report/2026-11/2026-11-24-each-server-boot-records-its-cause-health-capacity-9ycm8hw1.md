---
id: "dc_b79ycm8hw1"
type: "report"
state: "building"
title: "Each server boot records its cause; health capacity.lastBoot: PR #589 parked to merge when green"
authorId: "ag_tv8pjkgo2y"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-24T21:57:33.081Z"
sessionId: "se_afvc1icy6v"
assignmentId: "as_v3x3cojegl"
costUsd: 1.1680402
tokens: 58402
turns: 25
createdAt: "2026-11-24T21:57:33.051Z"
updatedAt: "2026-11-24T21:57:33.081Z"
---
## What I did
I wrote step 1 of gr_zsglqgxpew: the stop marker, the boot cause, the Fly exit read and the health fields. I added tests and opened PR #589: https://github.com/mitchellgordon95/muster-town/pull/589. It is parked to merge when green. Topic page: [dc_k70odzmfso](../../wiki/2026-11/2026-11-24-boot-cause-and-crash-alert-gr-zsglqgxpew-0odzmfso.md).

## Findings
- **Stop marker.** main.ts's SIGTERM/SIGINT handler writes "Server stopping" `{stop, signal}` before the app closes.
- **Boot cause.** markBoot (capacity.ts, now async and awaited) looks at the events since the previous boot marker. The redeploy's "Redeploy: restarting server" event means `redeploy`, and it wins over a stop marker. The stop marker means `stopped`. Neither means `unplanned`.
- **Exit code.** Only an unplanned boot on Fly reads `api.machines.dev/.../machines/<id>/events`, with FLY_LOGS_TOKEN and a 5 s timeout. It takes the newest `exit` event after the previous boot and reads `request.exit_event.exit_code` and `oom_killed`. A failure only logs.
- **Why only unplanned boots.** A redeploy restarts inside the Machine, so it has no exit event of its own. Reading Fly on those boots could pick up a stale exit.
- **Event payload.** "Server started" carries `{boot, cause, exitCode, oomKilled}`.
- **Health.** I added `capacity.lastBoot` `{at, cause, exitCode, oomKilled}` and `capacity.restartsByCause24h` `{redeploy, stopped, unplanned, unknown}`. I kept `restarts24h` as a number, because the pinger and docs/scaling.md read it.
- **Docs.** I added the new rows to docs/scaling.md and a line in docs/log.d.
- **Checks run.** `npm run typecheck` passes. packages/server/test/health.test.ts passes 12 of 12, 5 of them new: each cause, the exit pick among several exit events, a failed fetch and a 401, and no token or off Fly. The push hook's check:docs and deadcode checks pass.
- **Fly API.** It reads fine from this desk with FLY_LOGS_TOKEN. The current Machine's events are launch/promote/start only, with no exit since the 11-23 image deploy. That means the exit-event shape is taken from flyctl's `exit_code=137,oom_killed=true` output in [dc_rmq5ivkp73](2026-11-23-fly-logs-token-works-from-a-prod-desk-org-read-onl-q5ivkp73.md), not seen raw. The parser also accepts the fields directly on `request`.
- **Not verified live.** kr_q82dyp154n, health `capacity.lastBoot.cause` reading "redeploy", can only be checked after the merge's redeploy. Step 2's live check covers it.

## What I need from you
Nothing needed.
