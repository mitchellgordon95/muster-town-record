---
id: "dc_arbyy3hid2"
type: "report"
state: "building"
title: "PR #255 live in ba6cd93: a checkpoint retry keeps its system author; rollup 38 item 16 and retry rule written"
authorId: "ag_lb6ceww50b"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #255 live in ba6cd93, rollup 38 item 16 and retry rule on dc_mhz91klzjk written. Done."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T02:44:56.207Z"
sessionId: "se_qun1ju1gig"
assignmentId: "as_429hswdtro"
costUsd: 1.1063701000000001
tokens: 55319
turns: 23
createdAt: "2026-11-02T02:42:54.703Z"
updatedAt: "2026-11-02T02:44:56.207Z"
---
## What I did
I read GET /api/health at 2026-11-02T02:40:47Z. It shows commit ba6cd93, startedAt 02:40:36Z. `git merge-base --is-ancestor e992393 ba6cd93` succeeds, so PR #255 is **LIVE**. I read `retryAssignment` in core ops.ts at the live commit. Then I wrote the rollup 38 line on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) and the retry rule on [dc_mhz91klzjk](../../wiki/2026-10/2026-10-28-wakes-and-blocked-assignment-reasons-z91klzjk.md).

## Findings
- **Live code:** on ba6cd93, `retryAssignment` gives the copy `createdBy: isCheckpointAssignment(a) || !actor ? system : holderOf(actor)`. lanes.ts:118 lets only a checkpoint assignment run while its grant is at checkpoint, so a retried checkpoint report now runs instead of sitting "held: grant at checkpoint". That hold is what happened to as_9af14b4x6k at 02:19:12Z.
- **Not tested on a real retry.** No safe live probe exists: GET /api/assignments shows `createdBy: null`, and I retried nothing by hand. The gr_5ltmbf3a2f checkpoint is already in rollup 37 ([dc_zcuri3xdk2](2026-11-02-workshop-rollup-37-checkpoint-of-the-hosted-collec-uri3xdk2.md)). The core test in assignment-queue.test.ts covers both cases.
- **[dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md):** Pix 1 rewrote this page at 02:41:28Z, after I first read it, and added item 15 (#256). I rebased onto their version and added **item 16** (What it is / What you'd see / Your call: none; API-only, no picture; rollup 38 candidate). The header now records health ba6cd93. I re-read the page after writing: items 15 and 16 are both there.
- **[dc_mhz91klzjk](../../wiki/2026-10/2026-10-28-wakes-and-blocked-assignment-reasons-z91klzjk.md):** new line "Retry of a checkpoint assignment" with the rule, the live commit, the cause and the test.
- #256 (c322b25) is **not** in ba6cd93. Its live check is already parked elsewhere (item 15).

## What I need from you
Nothing needed.
