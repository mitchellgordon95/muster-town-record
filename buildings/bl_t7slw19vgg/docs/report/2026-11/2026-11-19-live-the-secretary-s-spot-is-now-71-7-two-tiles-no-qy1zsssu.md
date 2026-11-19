---
id: "dc_0nqy1zsssu"
type: "report"
state: "building"
title: "Live: the Secretary's spot is now (71,7), two tiles north (PR #508)"
authorId: "ag_9nrjxnjytb"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "For Mitchell, on the record of his flag \"nit: move the secretary's default position north a few tiles\": your nit is live. The Secretary now rests at (71,7), two tiles north of its old spot, still beside the hydrant at (70,11). PR #508 (c4293dec), live in 433b482 since 15:42 UTC; no custom spot overrides the new default. My redirect note wrongly asked the fork to `tell` you: `tell` reaches only agents and buildings (packages/core/src/verbs/social.ts:153-158), so this note is the record instead. The town files a \"Done\" notice for a flag only when the code settles its report itself (packages/core/src/verbs/docs.ts:397-402), not when the manager approves it; I have queued a fix so the next flag tells its human by itself."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-19T15:45:34.614Z"
sessionId: "se_lzqvh13zn4"
assignmentId: "as_ptykqzz01q"
costUsd: 0.6787016000000001
tokens: 33935
turns: 9
createdAt: "2026-11-19T15:43:02.417Z"
updatedAt: "2026-11-19T15:45:34.614Z"
---
## What I did
- Checked that live includes c4293dec. /api/health shows commit 433b4825 (started 2026-11-19T15:42:35Z), and `git merge-base --is-ancestor c4293dec 433b4825` succeeds.
- Read GET /api/town. The place desk:ag_7tiwyqva83, "Secretary's spot by the hydrant", is at (71,7). The Secretary ag_7tiwyqva83 stands at (71,7). The hydrant stays at (70,11).
- Tried to `tell` Mitchell (us_1la74k332n) one line. It was refused: `tell` reaches only agents and buildings, and a user id is neither.

## Findings
- Mitchell's flag [dc_hrm72814k5](../../flag/2026-11/2026-11-19-nit-move-the-secretary-s-default-position-north-a-m72814k5.md) is done on live. The default rest tile moved from (71,9) to (71,7), two tiles north, via PR #508 (c4293dec).
- No custom spot overrides it. The place record has no custom marker, and its position equals the new default.
- Line for Mitchell: "Your nit is live: the Secretary now rests at (71,7), two tiles north of its old spot, still beside the hydrant (PR #508)."

## What I need from you
Pass that line to Mitchell. A fork can't `tell` a human.
