---
id: "dc_1t4fp34nif"
type: "report"
state: "building"
title: "Pinger watch: PR #505 open, parked on CI"
authorId: "ag_xupyqnfewf"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T15:27:16.716Z"
sessionId: "se_l2wfkflsjy"
assignmentId: "as_4oxp5et45t"
costUsd: 1.3969414
tokens: 69847
turns: 27
createdAt: "2026-11-19T15:27:16.710Z"
updatedAt: "2026-11-19T15:27:16.716Z"
---
## What I did
Built gr_7tl5as3s0a step 1 in packages/server and opened draft PR #505 (https://github.com/mitchellgordon95/muster-town/pull/505). Parked on its CI.

## Findings
- **The change.** app.ts marks a `PingerWatch` on each GET /api/health whose user-agent starts with `muster-pinger`. The watch lives in memory and the Monitor owns it. Health gets `pinger {lastSeenAt, state ok|stale|none, staleAfterMin 15}`.
- **Monitor key `pinger`.** It goes red at once after 15 min with no probe, with no yellow stage. A pinger never seen since boot gives no reading and raises nothing. An open alert survives a restart. It clears after 5 samples once probes come back.
- **GET /api/health/pinger.** It answers 503 when stale, or when the state is none but the red alert is still open after a restart. Otherwise it answers 200.
- **Tests.** I added 4 tests to test/monitor.test.ts. monitor + health + backup tests pass locally: 71 tests, and typecheck is clean. The backup worker-thread test hit its 5 s timeout once in the full `check --fast` run. It passed when re-run alone, so it is a timing flake on the slow sandbox, not this change.
- **Docs.** I updated deploy/README.md (a table row and a "Pinger quiet" section), docs/architecture.md, and added a docs/log.d entry.

## What I need from you
Nothing needed.
