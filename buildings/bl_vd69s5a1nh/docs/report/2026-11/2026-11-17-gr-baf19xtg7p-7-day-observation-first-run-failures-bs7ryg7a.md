---
id: "dc_xtbs7ryg7a"
type: "report"
state: "building"
title: "gr_baf19xtg7p 7-day observation: first-run failures 17%, because the pre-push hook was never executable; fix in PR #499"
authorId: "ag_l9ku8ebnhc"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Measure again. The 11-10 to 11-17 window tested nothing: the hook never ran, so 17% is the baseline without a hook, not the hook's effect. as_9mam4njjra merges #499 when CI is green. A one-shot on the schedule (lane grant, 11-25 01:00Z) measures the 7 days after #499 went live and reports; the grant closes after that, with kr_o6jibyr7jj past its 11-19 due date either way, which only a human marks. Spend so far is well under the 300k ceiling."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-17T22:04:33.473Z"
sessionId: "se_pbjfb0ydxk"
assignmentId: "as_nmxhdnq0bw"
costUsd: 1.1800255
tokens: 59001
turns: 22
createdAt: "2026-11-17T22:03:43.733Z"
updatedAt: "2026-11-17T22:04:33.473Z"
---
## What I did
Measured the window from 2026-11-10 21:07Z to 11-17 21:07Z after PR #417, using the method on [dc_wp3isidhw8](../../wiki/2026-11/2026-11-05-pr-round-trips-ci-failures-and-merge-conflicts-3isidhw8.md). Found that the pre-push hook never ran on any desk. Fixed it in PR #499, https://github.com/mitchellgordon95/muster-town/pull/499 (draft, commit 84543ae5): chmod +x, a test that pins the mode, and a docs/log.d entry. Checked on a desk. Topic page [dc_wp3isidhw8](../../wiki/2026-11/2026-11-05-pr-round-trips-ci-failures-and-merge-conflicts-3isidhw8.md) is rewritten.

## Findings
- **The hook was dead.** #417 tracked `.githooks/pre-push` as mode 100644. Git skips a hook that is not executable ("hook was ignored because it's not set as executable"). So kr_5qrusz6ivw's earlier claim did not hold on any desk. After the fix, this branch's push ran the hook (passed in 56 s). A dry-run push of an unused export was refused (`pre-push: FAILED after 11s`, knip names `zzUnusedProbe`).
- **kr_o6jibyr7jj missed.** 81 PR branches had their first CI run in the window. 14 failed (17.3%) and 1 was cancelled. Over all PR runs, 15 of 99 failed (15%). The baseline was 13% (59 of 442) and the target is under 6%.
- **Failures by cause (14):**
  - knip: 8
  - check:docs, all the docs/manual.md 1900-word cap: 4. The manual is now at 1895 of 1900 words.
  - the "every test reading a repo file is in the fast map" test: 1 (teo-2)
  - docker build, git checkout in the image step: 1 (pix-3)

  The hook runs knip and docs, so 12 of the 14 would have been stopped on the desk.
- **kr_sbqqx7548z holds.** Of 55 merge commits in the window, which I read from PR heads, only 4d987b85 touches docs/log.md. That is PR #418 moving its pre-#417 line, 10 min after #417 merged, as the FYI said. There are none after it. docs/log.md is still at 355 lines, and check:docs still refuses an appended line (checked on the desk).
- **kr_vcv244638c holds.** 03364d14 is live: health is at 6096977b, and `merge-base --is-ancestor` succeeds. `check --fast` still fails at docs when manual.md goes over its cap.
- Next: merge #499 when CI is green. Then the hook's effect needs one more 7-day window after it is live, which falls past kr_o6jibyr7jj's due date of 11-19. I am parking on #499's CI so I can merge it.

## What I need from you
Nothing needed now. After #499 is merged, decide whether to measure again for 7 days or close the grant with kr_o6jibyr7jj marked missed.
