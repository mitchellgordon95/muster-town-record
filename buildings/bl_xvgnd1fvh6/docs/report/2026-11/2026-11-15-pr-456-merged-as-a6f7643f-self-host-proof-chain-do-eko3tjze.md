---
id: "dc_c9eko3tjze"
type: "report"
state: "building"
title: "PR #456 merged as a6f7643f: self-host proof chain done"
authorId: "ag_pt5kqawmlh"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged: PR #456 merged as a6f7643f on green, CI ships it. Self-host proof chain (as_uskv4clzoe → as_u770oxyn16) done. Nothing to queue; the do ask ak_w2a95k32je (destroy muster-town-selfhost, revoke FLY_SELFHOST_TOKEN) already waits on Mitchell."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-15T21:03:56.849Z"
sessionId: "se_4dzhp5onte"
assignmentId: "as_u770oxyn16"
costUsd: 0.2882521
tokens: 14413
turns: 7
createdAt: "2026-11-15T21:03:37.726Z"
updatedAt: "2026-11-15T21:03:56.849Z"
---
## What I did
PR #456's CI passed (check and image succeeded; promote was skipped, as it is on PRs). I marked the PR ready and merged it. I did not call redeploy: CI ships green main by itself.

## Findings
- PR #456 (https://github.com/mitchellgordon95/agent-town/pull/456) merged as **a6f7643ff519a70834d6778e8cf603bcadc9cce1**. It changes docs/self-host.md: an "On Fly.io" note, the live directory in section 6, and known gaps 4, 9 and 10. It also adds a docs/log.d entry.
- The self-host proof chain as_uskv4clzoe is complete. The proof itself is in [dc_2uz3nnvm1d](2026-11-15-self-host-proof-on-fly-live-admin-directory-verifi-z3nnvm1d.md). Topic page [dc_55z71al37g](../../wiki/2026-11/2026-11-04-self-host-image-gr-q1jrelx2ty-z71al37g.md) is updated.

## What I need from you
Nothing new: Mitchell's open ask ak_w2a95k32je (destroy the suspended app muster-town-selfhost and revoke FLY_SELFHOST_TOKEN) still stands.
