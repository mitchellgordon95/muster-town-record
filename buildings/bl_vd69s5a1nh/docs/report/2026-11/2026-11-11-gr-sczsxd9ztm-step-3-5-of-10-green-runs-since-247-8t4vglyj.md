---
id: "dc_ko8t4vglyj"
type: "report"
state: "building"
title: "gr_sczsxd9ztm step 3: 5 of 10 green runs since #247; tests 164 s, total 192 s, on course to miss ≤110/≤140; re-parked"
authorId: "ag_b4tce8kigs"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. 5 green main runs since aacc9fe6: tests median 164 s (152-175), total 192 s (175-204), against 220 / 249 s just before the merge: #247 cut CI tests by about 25%, but kr_0xk1ex7tus (tests at most 110 s, total at most 140 s) will miss by about 50 s and five more runs at plus or minus 15 s cannot close that. kr_9xqxj8v5cl claimed (aacc9fe6 is an ancestor of the live d30c6f8f). The grant is at its ceiling, so the parked continuation is held; the rollup asks Mitchell to cut it (recommended) or adjust it for the final 10-run read."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-11T02:02:45.248Z"
sessionId: "se_12wlstusas"
assignmentId: "as_nq3bi0pcti"
costUsd: 0.8132799999999998
tokens: 40664
turns: 9
createdAt: "2026-11-11T02:01:52.310Z"
updatedAt: "2026-11-11T02:02:45.248Z"
---
## What I did
I listed the main CI runs and read the `check:` line from every green run from aacc9fe6 (#247) on. I read 6 green runs from just before the merge to compare. I checked /api/health and rewrote the topic page [dc_87kealnkye](../../wiki/2026-10/2026-10-29-build-times-fast-check-kealnkye.md) with the table. Only 5 green runs exist so far: main has had no push since 21:43Z yesterday, and 4 runs were cancelled by newer pushes. So I am parking again to reach the 10 runs the key result names.

## Findings
- **kr_9xqxj8v5cl is met in practice.** /api/health at 01:59Z showed commit d30c6f8f. `git merge-base --is-ancestor aacc9fe6 d30c6f8f` succeeds. I claim it.
- **The 5 green runs from aacc9fe6 on** (42898563118, 42900011085, 42901842450, 42905320740, 42907870612):
  - Tests median **164 s** (range 152–175).
  - Total median **192 s** (range 175–204).
- **The 6 green runs just before the merge:** tests 220 s (205–227), total 249 s (232–259).
- **#247 cut CI test time by about 25%.** But the suite grew from 158 s on 11-06 to about 220 s before #247 landed. Against the 11-06 baseline the gain is only about 4% on tests.
- **kr_0xk1ex7tus (tests ≤110 s, total ≤140 s) is on course to miss.** The gap is about 54 s on tests and 52 s on total. Five more runs, which vary by about ±15 s, cannot close it. I mark it at-risk, not claimed.
- **What could still close the gap:** per-file cost in the core tests, which are half the tests step, or a bigger CI runner. Neither is in this grant's steps.
- **Next:** I resume after 20:00Z today, add the next green runs to make 10, file the final medians, and say the grant can close with kr_0xk1ex7tus missed.

## What I need from you
Nothing needed.
