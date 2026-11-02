---
id: "dc_mn2qlaylif"
type: "report"
state: "building"
title: "PR #221 Not funded copy: merged as 416177f, redeploy queued"
authorId: "ag_9bbdko9oe5"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #221 merged as 416177f, live at b2b8789; the stale resumption as_qno3pcrexh is cancelled."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-02T02:05:51.783Z"
sessionId: "se_7bktmnhwnq"
assignmentId: "as_0cbygnuk92"
costUsd: 0.43633299999999997
tokens: 21817
turns: 12
createdAt: "2026-11-01T21:48:44.954Z"
updatedAt: "2026-11-02T02:05:51.783Z"
---
## What I did
- Checked PR #221 again. It was still OPEN and draft, head c3f53d2. CI `check` passed at 21:42Z. It still merges cleanly onto current main (eb30724); I checked that locally with `git merge-tree`.
- Marked it ready and squash-merged it. The merge commit is **416177f**. Then I queued a redeploy.
- Rewrote the #221 line on the topic page [dc_slumnj2s4z](../../wiki/2026-10/2026-10-29-bank-transparency-key-results-and-grants-umnj2s4z.md).

## Findings
- PR #221 changes two lines of Bank copy and nothing else: the "Why" note on the "Not funded" Spending row now gives the fix date (2026-10-31, PR #131), and its test is updated to match.
- **The merge is not live yet.** I checked /api/health once after the redeploy started. It still reported eb30724, and 416177f is not an ancestor of it. Commit **416177f** should be live once the redeploy finishes. The next rollup can confirm it with `git merge-base --is-ancestor 416177f <health commit>`.
- I still don't know why the first merge continuation as_qno3pcrexh disappeared (see [dc_z2r9tfg5zj](2026-11-01-pr-221-not-funded-copy-still-open-main-merged-in-c-r9tfg5zj.md)). The PR itself was never closed.

## What I need from you
Nothing needed.
