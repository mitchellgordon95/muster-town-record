---
id: "dc_vvr35qv8ye"
type: "report"
state: "building"
title: "Grant gr_q1jrelx2ty adjusted: 600,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:137473:bl_xvgnd1fvh6"]
decision: "approve"
decisionNote: "Taken in: gr_q1jrelx2ty now 600,000 (333,785 spent). The held continuation as_etspipc4fa (path-B compose smoke, hourly backup to S3) unholds by itself; nothing re-queued."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-06T04:34:30.433Z"
createdAt: "2026-11-06T04:33:03.028Z"
updatedAt: "2026-11-06T04:34:30.433Z"
---
Written by the town: Mitchell adjusted grant gr_q1jrelx2ty at its checkpoint (event 137473, 2026-11-06 04:33 UTC).

## Summary

Grant gr_q1jrelx2ty "A stranger runs their own Muster Town with one `docker compose up` from a published image that CI builds, boots and backs up on every green main, with no human-provided test box." adjusted by Mitchell: 600,000 tokens.

Status funded; 333,785 of 600,000 tokens spent; key results kr_gec7ivzfxs [claimed] A published image: ghcr.io/mitchellgordon95/muster-town:prod and :<sha> are pushed by CI on every green main; kr_emrv9hzs47 [claimed] CI boots the image as docs/self-host.md path B says and it serves a fresh town that survives a restart; kr_nlbywt1hi4 [not-started] An hourly backup from the container lands in an S3 bucket and restores into a second container with the same agent count; kr_a4p4piyh7v [not-started] docs/self-host.md path B is pull-and-run: no clone or build, gaps #1 and #8 struck.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
