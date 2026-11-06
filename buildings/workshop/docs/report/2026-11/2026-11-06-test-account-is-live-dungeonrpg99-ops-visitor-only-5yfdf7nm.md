---
id: "dc_vv5yfdf7nm"
type: "report"
state: "building"
title: "Test account is live (dungeonrpg99-ops, visitor only): role reset + library skill queued (as_oj22fnltuz), gr_bwm0iz7rwl captain check queued behind it (as_a8rm855qrn), FYI updated"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_5bgy20qlvt","dc_fnqcknr8id","dc_ia2hybtuax","dc_f2vlvfz3mk"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged: the token is verified, the reset + skill (as_oj22fnltuz) and the gr_bwm0iz7rwl captain check (as_a8rm855qrn) are already queued, the FYI is updated and Kelly/Mara told. Nothing further to assign; rollup 51 carries the reset and skill once as_oj22fnltuz lands."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-06T04:32:37.714Z"
sessionId: "se_lo5zo2mjr5"
assignmentId: "as_em04v31q2t"
costUsd: 2.03870055
tokens: 101935
turns: 21
createdAt: "2026-11-06T04:32:13.671Z"
updatedAt: "2026-11-06T04:32:37.714Z"
---
## What I did
Read Mitchell's answer [dc_5bgy20qlvt](../../../../../library/human-report/2026-11/2026-11-06-re-create-a-second-github-account-for-testing-and-gy20qlvt.md) ("done") to the request [dc_fnqcknr8id](../../../../../town-hall/outbox/2026-11/2026-11-05-create-a-second-github-account-for-testing-and-giv-qcknr8id.md). Verified the secret from my desk, queued the work that waited on it, and told the buildings.

## Findings
- **The token works.** `MUSTER_TEST_GH_TOKEN` is in the Workshop desk environment. `POST /api/auth/github/device` with it returned a user bearer at 04:29Z (server clock). GET /api/me as that user: login **dungeonrpg99-ops**, id us_u4mzpz4zc7, roles `role:visitor` only, canInteract false, no pending join request, not admin. It is a never-granted stranger. Mitchell's answer did not name the account; the login comes from the API.
- **Queued, directed (sourceId [dc_5bgy20qlvt](../../../../../library/human-report/2026-11/2026-11-06-re-create-a-second-github-account-for-testing-and-gy20qlvt.md)): as_oj22fnltuz.** The role-reset step the FYI promised at first use (self-service reset to visitor: drop roles, captaincies except root, pending join and captain requests; admins refused; core + server tests, PR), plus a library skill "test-account-live-check" with the sign-in script and the one-check-at-a-time rule, then a live check. It reports the PR and skill id; I then update the FYI again.
- **Queued, grant gr_bwm0iz7rwl, waits for as_oj22fnltuz: as_a8rm855qrn.** Step 3 of "Ask to captain a goal", the end-to-end check that was blocked on a second human since 2026-10-31: ask to join if still a visitor, ask to captain a goal with a grant under it, then key-result evidence. Two clicks stay with Mitchell (let in, accept); they will come through the rollup's Needs line when the fork reports.
- **Town-wide FYI [dc_ia2hybtuax](../../../../town-hall/docs/fyi/2026-11/2026-11-05-outbox-rule-from-mitchell-2026-11-05-no-more-test-2hybtuax.md) rewritten** with an UPDATE block: the account, how to sign in, one live check at a time, reset pending, which outbox requests to withdraw and re-run. Told Kelly (Onboarding's join round trip goes first on the account) and Mara (withdraw [dc_y7jkfy8wav](../../../../../town-hall/outbox/2026-11/2026-11-03-register-a-test-visitor-on-a-full-building-s-goal-jkfy8wav.md) / dc_bn4s4m7cq3 and re-run); the town queued both tells as assignments for them.
- **Not re-run:** the Workshop's withdrawn request [dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md) (keyed collective check): Mitchell cut gr_5ltmbf3a2f at 04:23Z, and a keyed collective still needs a Console API key, a human's call.
- No rollup: rollup 50 was filed about 45 min ago and nothing new is live from this; rollup 51 carries the reset + skill once as_oj22fnltuz lands.

## What I need from you
Nothing needed.
