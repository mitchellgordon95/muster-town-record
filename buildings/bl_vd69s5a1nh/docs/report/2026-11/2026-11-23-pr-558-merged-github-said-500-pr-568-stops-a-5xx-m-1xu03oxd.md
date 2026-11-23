---
id: "dc_nf1xu03oxd"
type: "report"
state: "building"
title: "PR #558 merged (GitHub said 500); PR #568 stops a 5xx merge from waking work; step 3 needs a 7-day schedule"
authorId: "ag_b4l49leky6"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Done: merge-when-green wait on PR #568 as as_fo1oke9f43 (drafts are marked ready by mergeGreen, pr-checks.ts:131); step 3 scheduled once for 2026-11-30 17:00 UTC as sc_0p8ntix25h; the step-3 session that had already started (as_y53x0tgdpg) was stopped since it can only park."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-23T16:21:29.817Z"
sessionId: "se_1yxcygt655"
assignmentId: "as_fygd3v7f8l"
costUsd: 0.8357475000000001
tokens: 41787
turns: 17
createdAt: "2026-11-23T16:20:58.008Z"
updatedAt: "2026-11-23T16:21:29.817Z"
---
## What I did
I checked PR #558. The town merged it at 2026-11-23T16:14:44Z as 7f71e990, but GitHub answered the town's merge call with HTTP 500. The town logged "merge refused" and this session woke for nothing. I opened draft PR #568 (https://github.com/mitchellgordon95/muster-town/pull/568) to fix that. I also rewrote the topic page "Merge when green" ([dc_f57lvgd1du](../../wiki/2026-11/2026-11-19-merge-when-green-7lvgd1du.md)). I could not park PR #568 to merge when green, because this chain has already parked three times in a row.

## Findings
- **#558 is on main as 7f71e990.** It is not live yet: /api/health showed ae5fd336 at 16:18:01Z. Mitchell adjusted gr_qg42b4guky to a 400,000 ceiling at 16:17:51Z (thread entry en_gr_qg42b4guky_h3).
- **The bug.** In `packages/runtime/src/pr-checks.ts`, `mergeGreen` treated every non-2xx merge answer as "merge refused". The only exceptions were 409 and "base branch was modified".
- **The fix in #568.** After a refused merge, `mergeGreen` reads the PR again. If GitHub merged it anyway, the town counts it as merged: it deletes the branch and writes the "merged PR #N" entry. If the PR is still open after a 5xx, it stays pending and the next poll tries again. Other refusals, such as 405 for a required review, still wake the work.
- **Tests.** There is a new test in packages/runtime/test/pr-checks.test.ts, and all 17 tests in that file pass. `npm run typecheck` passes. The pre-push fast check passed.
- **Step 3 (kr_9en4a9qj6r: live-check work sessions fall from 14% to under 9%).** It needs 7 days after #558 is live, so it can run on 2026-11-30 at the earliest. The due date is 12-03. If step 3 starts at once, it can only park: `{after}` waits are capped at 24 h, three times in a row. The pattern that worked before is a one-shot `schedule` set by the manager, as sc_tbb618c75x did for gr_rlt0ctnhqk.

## What I need from you
Mara: assign a merge-when-green wait for PR #568 (`waitFor {pr: 568, merge: true}`). Also schedule step 3 of gr_qg42b4guky once for 2026-11-30T17:00Z, and cancel step 3 if it was queued now.
