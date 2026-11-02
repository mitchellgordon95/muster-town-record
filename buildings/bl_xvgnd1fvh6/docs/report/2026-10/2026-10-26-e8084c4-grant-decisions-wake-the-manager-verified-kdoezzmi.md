---
id: "dc_cekdoezzmi"
type: "report"
state: "building"
title: "e8084c4 (grant decisions wake the manager) verified live on muster.town: health commit 8a39682 contains it and the live manager prompt names the fund / counter / reject wakes; nothing to change"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_50fai9onl1"],"urls":["https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Verified live; as_t8ag8kacyd fully done. Nothing further; next exercise of the hook is Mitchell's decision on gr_jkorz4f49a."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-26T21:07:45.142Z"
sessionId: "se_hopm00se8a"
assignmentId: "as_f6bfifiogd"
costUsd: 0.7605295000000001
tokens: 9145
turns: 8
createdAt: "2026-10-26T21:07:32.841Z"
updatedAt: "2026-10-26T21:07:45.142Z"
---
## What I did
Resumed as_f6bfifiogd after the redeploy. Fetched main, read `commit` from https://muster.town/api/health, ran `git merge-base --is-ancestor e8084c4 <live>`, and checked the live manager prompt (my own session prompt, served by the live server) for the grant-decision wake text. No code change, so no PR and no redeploy.

## Findings
- **Live commit:** 8a39682 (health `commit`). `git merge-base --is-ancestor e8084c4 8a39682` succeeds, and e8084c4 is on origin/main.
- **Manager prompt:** the live prompt carries the paragraph "A human's decision on your proposal wakes you with an assignment, like a reply to a report: funded → "Grant … funded: assign its first step or take it yourself" …, countered → "Answer the counter on …" …, rejected → "Grant … rejected: read the note"." Source: packages/core/src/prompts.ts; the hook is `Grants.decisionAssignment` in packages/core/src/grants.ts (lines 371, 388, 401 build the three titles); docs/wakes.md lists `grant.funded` → manager assignment.
- The original assignment as_t8ag8kacyd (Mitchell's 1:1 ask) is therefore fully done: shipped, tested, live, verified. The next real exercise of the hook is Mitchell's decision on the open backup proposal gr_jkorz4f49a, which should wake me with one of those three assignments.

## What I need from you
Nothing needed.
