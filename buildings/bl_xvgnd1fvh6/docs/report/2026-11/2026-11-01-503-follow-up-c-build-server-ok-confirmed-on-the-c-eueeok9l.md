---
id: "dc_4zeueeok9l"
type: "report"
state: "building"
title: "503 follow-up C: \"build server … ok\" confirmed on the c1cdd23 CI redeploy (0.76 s)"
authorId: "ag_kv2zlnojow"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "503 follow-up C confirmed live: \"build server … ok\" on the c1cdd23 CI redeploy (0.76 s), npm install skipped, CI debounce held (one restart, 25.8 min after the previous). Fast-boot \"after\" number waits on the image deploy (outbox dc_lyjnyeev9f, do not re-ask). Goes in rollup #28 with the CI-debounce \"Your call\"."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T01:01:19.244Z"
sessionId: "se_dyzra67o1b"
assignmentId: "as_6pquvsdieq"
costUsd: 0.3337771
tokens: 16689
turns: 5
createdAt: "2026-11-01T01:01:05.833Z"
updatedAt: "2026-11-01T01:01:19.244Z"
---
## What I did
- Read /api/health and /api/events, then updated the topic page [dc_eka5xluv6o](../../wiki/2026-11/2026-11-01-prebuilt-server-and-ci-redeploy-coalescing-a5xluv6o.md).

## Findings
- **The "build server" step works.** The first redeploy run from 97911e8 code was CI's ship of c1cdd23. Its events (90074–90111) show "Redeploy: build server …" at 00:56:13.342Z and "… ok" at 00:56:14.101Z, so the build took 0.76 s. The same run shows "npm install … skipped (package-lock.json unchanged)".
- **c1cdd23 is live.** health.commit is c1cdd23 and startedAt is 00:58:18Z. backup.lastAt == verifiedAt at 01:00:07Z and error is null.
- **The CI debounce held.** CI asked for the redeploy at 00:56:05Z, 25.8 min after the previous start, and it was the only restart. The drain waited 2 min for Pix's meeting session.
- **Boot time is still the tsx path.** Restarting → finished took 3.1 s, against 2.9 s on 00:30. The image entrypoint that starts the prebuilt bundle needs the town image deploy, which is already asked for in outbox [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md). After that deploy, the restarting → finished gap is the "after" number. The desk estimate for the bundle was 0.87 s of CPU to first health.
- This part of follow-up C is done.

## What I need from you
Nothing needed. The image deploy is already in the outbox ([dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md)). PR #230's CI change applies town-wide, so the CI debounce veto stays in the rollup's "Your call".
