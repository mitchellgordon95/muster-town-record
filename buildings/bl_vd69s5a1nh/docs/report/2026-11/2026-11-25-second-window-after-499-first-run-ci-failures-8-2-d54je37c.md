---
id: "dc_gid54je37c"
type: "report"
state: "building"
title: "Second window after #499: first-run CI failures 8.2% (8 of 97), knip and docs 0; check:css fix in PR #601"
authorId: "ag_xh93ezxhtp"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Passed up to the humans as ask ak_9k40sjwg7i: Second window read done. kr_o6jibyr7jj came in at 8.2% (7.3% without the deliberate #580), above the 6% target: only a human marks it missed, so the key result goes to Mitchell as a click ask. The grant stays funded until he decides; then I close it (close_grant would otherwise mark the KR met). PR #601 merges itself (as_favuo21lnv waits on it). Nothing queued."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-25T01:06:57.780Z"
sessionId: "se_z1it26xiww"
assignmentId: "as_1t93hv781y"
costUsd: 1.0761703000000002
tokens: 53809
turns: 24
createdAt: "2026-11-25T01:04:07.395Z"
updatedAt: "2026-11-25T01:06:57.780Z"
---
## What I did
Measured 2026-11-17 22:16Z → 11-24 22:16Z. PR #499 merged at 22:09:50Z as cbfa71ee, and main CI finished at 22:15:38Z. I used the method on [dc_wp3isidhw8](../../wiki/2026-11/2026-11-05-pr-round-trips-ci-failures-and-merge-conflicts-3isidhw8.md). I read each failed first run's log. I confirmed on my desk that a push runs the hook. Then I fixed the one failure class the hook could catch but missed: PR #601 (https://github.com/mitchellgordon95/muster-town/pull/601), parked to merge when green.

## Findings
- **kr_o6jibyr7jj:** 97 PR branches had their first CI run in the window. 83 passed, **8 failed (8.2%)** and 6 were cancelled. Leaving out the throwaway PR #580, which was red on purpose, it is 7 of 96 (7.3%). Comparison: target under 6%, baseline 13% (59/442), no-hook window 17.3% (14/81).
- **Failures by cause:**
  - knip 0 (was 8) and check:docs 0 (was 4). The hook removed both classes.
  - check:css 2 (#535, Nell 1's balance tab). It was a CI-only step.
  - Docker image 2 ("fatal: not a git repository" in the Dockerfile RUN, teo-2 and nell-1). Each passed on its next run. This is a CI context issue, not something a desk can catch.
  - Tests 3: #506 keyResults.test and #555 redeploy.test were real failures outside the push's tests; #579 was the export-import timing flake.
  - Intentional 1 (#580).
- **Hook runs:** `.githooks/pre-push` is 100755 on main. My desk's `git push --dry-run` printed `check --push: docs 1s | deadcode 9s | typecheck 40s`, passed in 52 s. The push of #601 also ran it. Earlier reports also mention the hook passing ([dc_sax2bni2mi](../../../../bl_6ifesdbah3/docs/report/2026-11/2026-11-16-fix-for-boot-retired-request-cards-in-pr-479-parke-x2bni2mi.md)).
- **PR #601:** `npm run check`'s docs step now runs check:css after check:docs. I removed CI's separate step and added a test, "pre-push hook › runs check:css with the docs step". Checked on the desk: a stray `font-size:13px` makes `npm run check -- docs` fail at docs; check-scripts tests pass 13/13 and typecheck passes. This alone would have made the window 6 of 97 (6.2%).
- **kr_sbqqx7548z holds:** no commit on main after 4d987b85 touches docs/log.md, and no merge commit in the window touches it. log.md is at 355 lines and docs/log.d has 177 files.
- **kr_vcv244638c holds:** 03364d14 and cbfa71ee are both ancestors of the live commit 2be107b4 (/api/health, started 2026-11-24 22:56:16Z).
- Topic page [dc_wp3isidhw8](../../wiki/2026-11/2026-11-05-pr-round-trips-ci-failures-and-merge-conflicts-3isidhw8.md) rewritten.

## What I need from you
Close; kr_o6jibyr7jj is at 8.2% (7.3% without the deliberate #580), above 6%, a human marks it missed.
