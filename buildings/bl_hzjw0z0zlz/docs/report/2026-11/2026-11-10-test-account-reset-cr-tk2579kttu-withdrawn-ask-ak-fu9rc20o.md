---
id: "dc_wofu9rc20o"
type: "report"
state: "building"
title: "Test account reset: cr_tk2579kttu withdrawn, ask ak_o2d8ip3gjw retired"
authorId: "ag_d6dueshiix"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. Reset did the one thing it was for: captainRequestsWithdrawn 1, ak_o2d8ip3gjw retired at 22:09:04Z, account back to visitor-only and free. Nothing further."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-10T22:09:41.054Z"
sessionId: "se_5yoztx4ldc"
assignmentId: "as_hlhdb99xud"
costUsd: 0.48798030000000003
tokens: 24399
turns: 14
createdAt: "2026-11-10T22:09:26.108Z"
updatedAt: "2026-11-10T22:09:41.054Z"
---
## What I did
- Signed in as the test account (dungeonrpg99-ops, us_u4mzpz4zc7) with the skill script from [dc_11e758uhzj](../../../../../library/skill/2026-11/2026-11-06-test-account-live-check-e758uhzj.md). Its state was what we expected: visitor-only, and the event log showed no other building's check on it.
- Called POST /api/me/reset, then checked /api/me, /api/asks and the event log.
- Told Pix that the account is free. Updated the Gaps seen section of topic page [dc_ngm3fxpcq5](../../wiki/2026-11/2026-11-10-three-doors-gr-y9bpvx197c-m3fxpcq5.md).

## Findings
- **Reset response (HTTP 200):** `captainRequestsWithdrawn: 1`. Everything else was empty or 0 (rolesRemoved, goalsReleased, accessRequestsDeleted, directGrantsRemoved, agentsRetired).
- **The ask is gone:** the event log has `ask.retired` at 22:09:04Z for "Make @dungeonrpg99-ops captain of 'Collectively funded'", with the note "Withdrawn: the asker reset their account." GET /api/asks no longer lists ak_o2d8ip3gjw or cr_tk2579kttu. Before the reset it listed ak_o2d8ip3gjw as open. Mitchell has nothing to decide on it.
- **Account state after (GET /api/me):**
  - Roles: role:visitor only.
  - isAdmin false, canInteract false.
  - accessRequest null.
  - No captaincy, no direct goals, no live visitor agents.
- The live server was on d30c6f8f.
- I did not touch the older stale asks ak_nrdhhq656e and ak_aj5by41aya, which were out of scope.

## What I need from you
Nothing needed.
