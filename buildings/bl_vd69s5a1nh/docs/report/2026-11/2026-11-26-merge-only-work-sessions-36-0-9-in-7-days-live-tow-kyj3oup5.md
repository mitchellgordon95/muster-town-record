---
id: "dc_z2kyj3oup5"
type: "report"
state: "building"
title: "Merge-only work sessions 36% → 0.9% in 7 days live; town merged 74 PRs; all three KRs have evidence"
authorId: "ag_gsjquax53t"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 3's 7-day window is measured: merge-only work sessions 2 of 212 (0.9%) against 36% baseline; 74 PRs merged by the town with no session; 10 wakes each carry their reason. All three KRs have evidence; closing gr_rlt0ctnhqk as done. Nothing queued."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-26T16:03:39.619Z"
sessionId: "se_09alsc1129"
assignmentId: "as_y9xkq97off"
costUsd: 1.6655133
tokens: 83276
turns: 29
createdAt: "2026-11-26T16:03:18.148Z"
updatedAt: "2026-11-26T16:03:39.619Z"
---
## What I did
I read the 7-day window from 2026-11-19 15:50Z to 11-26 15:50Z. `/api/sessions` stops at 200 rows and has no paging. Forks also get a new agent id each time, so reading it per agent left out 11-19 to 11-22. Instead I paged `GET /api/events?since=` from id 173501 (11-19 15:41Z) to the end of the window, 18,065 events. From them I kept the `session.started` events with purpose work. For each one I read the assignment's title, description and report, plus the `pr.merged` events and the wake events. I also read thread jb_gr_rlt0ctnhqk. Topic page [dc_f57lvgd1du](../../wiki/2026-11/2026-11-19-merge-when-green-7lvgd1du.md) is rewritten and records the method.

## Findings
- **kr_vluzm4hto9 (merge-only work sessions under 10%): 0.9%, against 36% before.**
  - Window totals: 212 work sessions, plus 153 manage and 39 estimate sessions.
  - **Strict count: 2 of 212.** Teo's "If PR #515 is green, mark it ready and squash-merge it…" (as_hdyxntnctx, 13,030 adj.) and the same for PR #516 (as_c6mx77fqqf, 10,911 adj.). Both ran at 11-19 16:00Z. They were parked with a plain {pr: N} before step 2 taught merge: true. After 11-19 no title asks an agent to merge a green PR.
  - **Broad count: 4 of 212 (1.9%).** This adds the PR #558 HTTP 500 wake (as_fygd3v7f8l, 41,787 adj.; the PR was already merged, and PR #568 now stops this) and Prod's timed re-check that parked PR #582 (as_1quhyvj10e, 11,832 adj.).
  - Baseline: 42 of 117 (36%) in [dc_8zvfwxreid](2026-11-19-proposed-gr-rlt0ctnhqk-the-town-merges-green-prs-i-vfwxreid.md).
- **kr_zid82iurqe (the town merges with no session).** Over the 7 days the town merged 74 PRs, #512 to #601, across 7 buildings. 74 `pr.merged` events carry payload.by "town", and 74 thread entries read "merged PR #N as <sha8>". The first is en_as_abip30ogvl_merged on jb_gr_rlt0ctnhqk (moved {kind: merged, pr: 512, sha: e5f33c67, by: town}, at 2026-11-19T15:48:55Z).
- **kr_lse9k08ixi (red, conflict and refused-merge PRs wake with the reason).** 10 parks woke during the window. Each wake has a matching `assignment.status` event "…town to merge it (failed: <reason>)", and the reason was written into the assignment:

| Reason | PRs and what the woken session did |
|---|---|
| check (4) | #535 check:css fixed; #555 test fix; #579 flaky timing test, merged main to rerun; #590 check:css fix |
| merge conflict, CI did not run (3) | #537, #542, #557: each resolved and parked again |
| image job (2) | #547 closed as a duplicate of #546; #550 image flake retriggered with an empty commit |
| merge refused: HTTP 500 (1) | #558: GitHub had merged it, so the wake was not needed; PR #568 fixed this |

  No 5xx wake came after #568. Each woken session spent 15k to 42k adj. tokens.
- **Leftover toil, not merge-only:** 3 of the 10 wakes were CI flakes, not code faults (#550 image, #579 timing, #547 image). Grant proposal gr_4ld3zbxvrf already covers the image flake.

## What I need from you
Nothing needed. Mara runs close_grant on gr_rlt0ctnhqk with the evidence above.
