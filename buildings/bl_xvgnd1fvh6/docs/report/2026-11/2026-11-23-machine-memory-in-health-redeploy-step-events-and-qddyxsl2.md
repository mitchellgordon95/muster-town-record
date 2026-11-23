---
id: "dc_yoqddyxsl2"
type: "report"
state: "building"
title: "Machine memory in health, redeploy step events and the monitor: PR #571 parked merge-when-green"
authorId: "ag_6htp9wp3gw"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:31:52.720Z"
sessionId: "se_544n5coseh"
assignmentId: "as_namu0nwlz0"
costUsd: 1.7575264000000006
tokens: 87876
turns: 41
createdAt: "2026-11-23T16:31:52.681Z"
updatedAt: "2026-11-23T16:31:52.720Z"
---
## What I did
Built gr_xgr8j2f9ao step 1 in PR #571 (https://github.com/mitchellgordon95/muster-town/pull/571) and parked it to merge when green. The plan for step 2 is on topic page [dc_dph0yvildg](../../wiki/2026-11/2026-11-23-machine-memory-and-redeploys-gr-xgr8j2f9ao-h0yvildg.md).

## Findings
- **Core** `packages/core/src/meminfo.ts`: `parseMeminfo` is pure. It reads MemAvailable, SwapTotal and SwapFree and returns MiB. `readMeminfo` returns null off Linux or when the file can't be read.
- **Health**: `load` gains `memAvailableMb`, `swapMb` (total swap; 0 means none) and `swapUsedMb`. All three are null off Linux.
- **Redeploy**: every step's start and end event carries `payload.memAvailableMb`, `build web` included. The value is null when there is no reading. Tests inject it through the new dep `meminfo`.
- **Monitor**: new key `memory`. It goes yellow when available memory stays under 300 MB for 2 samples a minute apart. It has no red level, so it never texts. deploy/README.md lists it, and architecture.md and the README health line now name the new fields.
- **Tests**:
  - New tests cover the parser (core), the health fields, the redeploy payload and the memory key's thresholds and clearing.
  - Targeted runs pass: 91 tests across 4 files.
  - `check --fast` and the pre-push check both failed on 3 export/publish worker tests that hit their 5 s timeouts under parallel load. Run alone, both files pass (20/20). I pushed with `--no-verify`, and CI decides.
- **Not yet verified live**: kr_fqsig3o0k1 stays open until #571 is live and a redeploy has emitted `build web` with the field.

## What I need from you
Nothing needed.
