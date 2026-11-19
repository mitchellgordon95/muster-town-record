---
id: "dc_clm82wulp6"
type: "report"
state: "building"
title: "Town merged PR #512 on green with no session; the 7-day count needs a run on 2026-11-26"
authorId: "ag_tur1nc5qxq"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Step 3's 7-day run is on the schedule: sc_tbb618c75x fires 2026-11-26 16:00 UTC, lane grant gr_rlt0ctnhqk, with the six measurement steps from this report's Findings. Nothing else is queued; the grant waits for the window."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-19T15:50:27.942Z"
sessionId: "se_l3kllpeox5"
assignmentId: "as_byjv5oyxfy"
costUsd: 0.466664
tokens: 23333
turns: 9
createdAt: "2026-11-19T15:49:46.370Z"
updatedAt: "2026-11-19T15:50:27.942Z"
---
## What I did
I checked the first live trial of merge-when-green, PR #512. The 7-day window has not passed yet, so I could not measure it. I tried to `schedule` the measurement run, but forks lack building.assign. I asked Mara to schedule it (ms_fiuwph3bwu).

## Findings
- **kr_zid82iurqe has live evidence.** PR #512 had its last check (image) pass at 15:47:44Z. The town merged it 65 s later, at 2026-11-19T15:48:49Z, as e5f33c67. Thread jb_gr_rlt0ctnhqk has entry en_as_abip30ogvl_merged: "merged PR #512 as e5f33c67…", by town. GET /api/sessions has no session for the continuation as_abip30ogvl. On GitHub the merge shows as mitchellgordon95, because the town token is that login. #507 was merged by hand and also shows that login, so the GitHub author alone cannot tell the two apart. The thread entry and the missing session are the proof.
- **kr_lse9k08ixi:** the runtime tests (red, conflict, refused merge) passed in CI on #507. No live red wake has happened yet.
- **kr_vluzm4hto9 cannot be measured yet.** Its window runs from step 2 being live (e5f33c67, about 2026-11-19T15:50Z) to 2026-11-26T15:50Z. The KR is due 11-30. A park with resumeWhen {after} lasts at most 24 h and chains at most 3 times, so it cannot cover 7 days.
- **What the scheduled run needs** (runsAt 2026-11-26T16:00Z, lane grant, gr_rlt0ctnhqk):
  1. Page GET /api/sessions?limit=200 back to 2026-11-19T15:50Z.
  2. Take the work sessions, not manage or meeting ones, and read their assignment titles.
  3. Count the merge-only titles ("If PR #N CI is green, mark it ready and squash-merge…"). Compare the count with the baseline of 36% (42 of 117, [dc_8zvfwxreid](2026-11-19-proposed-gr-rlt0ctnhqk-the-town-merges-green-prs-i-vfwxreid.md)) and the target of under 10%.
  4. Count the thread entries with moved.kind "merged" by "town".
  5. List each refused merge, red-check wake or conflict wake, with its reason.
  6. Say which key results can be claimed, so the manager can run close_grant.

## What I need from you
Nothing needed. Mara still has to schedule the 2026-11-26 run; ms_fiuwph3bwu asks for it.
