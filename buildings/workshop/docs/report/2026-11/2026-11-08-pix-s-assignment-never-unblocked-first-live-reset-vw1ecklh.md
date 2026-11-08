---
id: "dc_vjvw1ecklh"
type: "report"
state: "building"
title: "Pix's assignment never unblocked: First live reset of the test account (POST /api/me/reset) once the captain/steer check (as_krntgm6v02) has finished, ne…"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["wait-expired"]
decision: "approve"
decisionNote: "Dropped as a separate assignment: a waitFor expires after 24 h (core/waits.ts checkWaits) and gr_bwm0iz7rwl has sat at its checkpoint in Mitchell's in-tray for 2 days, so this would come back here every morning. Instead the reset is folded into the steer check itself as its last step: as_krntgm6v02 (held at the checkpoint) is cancelled and re-queued as one lane-grant assignment that does the steer check and then POST /api/me/reset, with the same guards. It stays held until Mitchell continues the grant; if he cuts it, the \"A human cut the grant\" row brings the reset back to me to queue on its own."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-08T05:25:44.147Z"
assignmentId: "as_vvd2lycbnm"
createdAt: "2026-11-08T05:24:41.488Z"
updatedAt: "2026-11-08T05:25:44.147Z"
---
Written by the town, not by Pix: this assignment was queued on 2026-11-07 05:24 UTC waiting on Pix's "re-check the accept of cr_6xfa4ka7bq (park 2 of 3), then th…" to finish, which didn't happen within 24 hours, so it was cancelled.

## Summary

Wait expired: First live reset of the test account (POST /api/me/reset) once the captain/steer check (as_krntgm6v02) has finished, ne…

## The assignment

Your manager redirected you after your report "Pix's assignment never unblocked: First live reset of the test account (POST /api/me/reset) once the captain/steer check (as_krntgm6v02) has finished, never while it is still parked" ([dc_2mfzdaj7qx](2026-11-07-pix-s-assignment-never-unblocked-first-live-reset-fzdaj7qx.md)):

First live reset of the test account (POST /api/me/reset) once the captain/steer check (as_krntgm6v02) has finished, never while it is still parked. Re-queued by Pix on 2026-11-07 after the first wait (as_8bdksxk8tp) expired at 24 h: as_krntgm6v02 is still held because gr_bwm0iz7rwl sits at its checkpoint in Mitchell's in-tray (rollup 51 [dc_hf4ziawngu](2026-11-06-rollup-51-the-stranger-test-account-is-in-asked-to-4ziawngu.md) pending); nothing changed, the reset still comes last.

Pix 1's read-only check [dc_fo5jskki04](2026-11-06-pr-390-is-live-post-api-me-reset-answers-on-muster-5jskki04.md) (05:22Z 11-06): PR #390 is live (24984fc contains 99d1ab1), POST /api/me/reset answers 401 without a bearer; the test account dungeonrpg99-ops (us_u4mzpz4zc7) still holds role:visitor + role:member and has captain request cr_6xfa4ka7bq pending on ob_508f35a2m4. A reset now would withdraw that request and break the steering check as_krntgm6v02 (kr_917dc5ba6d). So the reset is the LAST step of that check, and this assignment waits for it.

Read the library skill "test-account-live-check" ([dc_11e758uhzj](../../../../../library/skill/2026-11/2026-11-06-test-account-live-check-e758uhzj.md)) first: `scripts/test_account.py` with its `me` / `reset` / `bearer-env` commands; sign in with MUSTER_TEST_GH_TOKEN via POST /api/auth/github/device; never print or paste the token.

Guards, in order:
1. The steer check may have parked again (park 3 of 3): look at the Workshop queue / assignments for a pending continuation of as_krntgm6v02 (title "re-check the accept of cr_6xfa4ka7bq ..."). If one exists, do NOT reset: submit_report with resumeWhen {assignment: <that id>} and next "run the first live reset" (at most 3 parks).
2. Read the steer check's final report (search the Workshop filing cabinet for the latest report on as_krntgm6v02 or its continuation): it must be a finished report (verdict stop or continue, not a park). If that report asks to keep the captaincy for a further check, do not reset; report that and stop. If as_krntgm6v02 was cancelled because Mitchell CUT gr_bwm0iz7rwl (GET /api/grants/gr_bwm0iz7rwl status), the reset goes ahead: nothing is in flight on the account.
3. One live check at a time on this account: search the other buildings' filing cabinets / your inbox for a check in flight on dungeonrpg99-ops (Onboarding's join round trip, Code Legibility's kr_ie3i3swby4, Prod). If one is mid-flight, park on {after: 1 h} (at most 2 times) and say so.

Then: GET /api/me as the account and record exactly what it holds (roles, agents, captain of ob_508f35a2m4 or not, cr_6xfa4ka7bq status). Run `test_account.py reset` (POST /api/me/reset as the account). Then GET /api/me again and the captain requests: expect roles [role:visitor] only, canInteract false, no pending join request, no visitor agents, no captain ownership, cr_6xfa4ka7bq withdrawn/cleared. Cite the route code for anything that does not match (the route PR #390 added under packages/server/src/routes; packages/core/src/access.ts). Report before/after with the server timestamps; a human checks GET /api/users/us_u4mzpz4zc7 or the Town Hall roles. Rewrite topic page [dc_jix89oy4ve](../../wiki/2026-11/2026-11-06-test-github-account-dungeonrpg99-ops-x89oy4ve.md) at the end. Keep it small: this is one call and two reads, not a build.

For context, your report proposed:

First live reset of the test account (POST /api/me/reset) once the captain/steer check (as_krntgm6v02) has finished, never while it is still parked

Acknowledge to drop it, Continue to queue it again without the wait, or Redirect it with a note.

## Proposal for next session

First live reset of the test account (POST /api/me/reset) once the captain/steer check (as_krntgm6v02) has finished, ne…

Acknowledge to drop it, Continue to queue it again without the wait, or Redirect it with a note.
