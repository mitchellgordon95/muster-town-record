---
id: "dc_tsgjmkz9ki"
type: "report"
state: "building"
title: "One agent model, step 2 is live (PR #281, 19bafad in 66e5d33): a visitor registers on a goal and gets a desk beyond the headcount that never takes a fork slot; contributed tokens need your go-ahead"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_4dhbi0sbgz","dc_k4pndkmh4s"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_jkas7hj80f"
createdAt: "2026-11-03T18:02:21.308Z"
updatedAt: "2026-11-03T18:02:21.308Z"
---
Live: 66e5d33 (contains our 19bafad), since /api/health startedAt 2026-11-03T04:17:48Z.

## Shipped
**1. One agent model, step 2: visitors pick a goal and get a desk beyond the headcount**
**What it is:** Grant gr_a5ct690l7a, KR kr_ie3i3swby4. PR #281 (merged as 19bafad). "Connect your agent" now registers a visitor on a goal (`goalId`; `buildingId` still works as an alias): the visitor is homed in the lab on that goal or the nearest goal above it, and gets the lowest free desk at or above the headcount (`claimDesk(.., {visitor: true})`, core world/map.ts:151-166). `deskCount` leaves visitor desks out (core world/map.ts:203-209), so everything built on it (freeDesks, fork spawning, exploration's "no free desk" check, the goal tree's inUse) ignores them: a visitor never takes a fork slot and the headcount never changes. When the presence sweep marks a visitor offline the desk is released and the body goes to the bench; coming back claims one again. A goal with no lab on its chain refuses with 409 "no desks to join yet" (step 4's adopt verb replaces that). Core tests cover claim beyond headcount, fork not blocked, register on goal/sub-goal/409, release on offline, map re-lot with no overlap; invariants 8–9 added to docs/invariants/agent-lifecycle.md. Reports [dc_k4pndkmh4s](2026-11-03-gr-a5ct690l7a-step-2-pr-281-merged-19bafad-visitor-pndkmh4s.md), [dc_4dhbi0sbgz](2026-11-03-gr-a5ct690l7a-step-2-live-19bafad-in-66e5d33-a-vis-hbi0sbgz.md).
**What you'd see:** Bank Transparency (headcount 3) holds 3 desks: Nell, fork Nell 1 and the offline visitor ag_dqylyrzxtx (registered before #281), while GET /api/goals shows inUse 2 for its goal (read 2026-11-03T18:00Z). Before the deploy the same visitor counted as a slot and Nell could not spawn a fork. No picture: the goal-tree count is the visible change. Not built: "contributed" tokens on the goal page (see Needs).
**Your call:** Register a test visitor on a full building's goal from Connect your agent (Prod's goal, both desks in use) and check the visitor gets a desk and Prod's inUse stays 2/2 (agents can't: POST /api/agents/visitors needs a signed-in user).

Queued now: step 4 (kr_8a7vskwse2, as_t5zobjg73s): the adopt verb, a visitor adopting a goal with no desks becomes its building's manager. Capped at ~120k; KRs 1–3 live already satisfy the stop condition, so if it runs large the fork stops at a clean point and I close the grant with what is live.

## Decided
- [dc_4dhbi0sbgz](2026-11-03-gr-a5ct690l7a-step-2-live-19bafad-in-66e5d33-a-vis-hbi0sbgz.md) → approve (step 2 verified live: 3 desks vs inUse 2 at Bank Transparency; step 4 unblocked)
- [dc_k4pndkmh4s](2026-11-03-gr-a5ct690l7a-step-2-pr-281-merged-19bafad-visitor-pndkmh4s.md) → approve (PR #281 merged as 19bafad; contributed tokens held for your go-ahead, not started)

## Key results
Grant gr_a5ct690l7a "One agent model" (funded 1,000,000; roughly 700k at the last rollup + 131,952 for the step-2 PR session + the live-check session ≈ 850k):

| Key result | Status | Evidence |
|---|---|---|
| kr_lrjhxy0pea moderator, reviewer, residents list, Ada gone (due 11-07) | at-risk in the town; LIVE since 024b236 | /api/town no Ada, /api/roles no moderator/reviewer ([dc_cuygorz7ae](2026-11-02-one-agent-model-ada-moderator-and-reviewer-roles-a-ygorz7ae.md)) |
| kr_p6nsa3zknw status transition table + isGone + stop guard (due 11-07) | not-started in the town; LIVE since 6e6d663 | STATUS_TRANSITIONS in schema, 4 lifecycle tests green, stop on a retired agent → 409 ([dc_7j4ar9jgty](2026-11-03-one-agent-model-step-3-is-live-pr-269-6e6d663-agen-4ar9jgty.md)) |
| kr_ie3i3swby4 visitor desk beyond headcount (due 11-07) | not-started in the town; LIVE since 19bafad, minus contributed tokens | 3 desks held vs inUse 2 at Bank Transparency; core tests for claim/release/not-a-fork-slot; contributed tokens not built (no data exists) |
| kr_8a7vskwse2 adopt verb for a goal with no desks (due 11-10) | not-started; queued as_t5zobjg73s | — |

Today's spend by lane: exploration 65,339 tokens (free under the goal: 97,865), directed 118 tokens.

## Needs from Mitchell
1. Go or no-go on "contributed" visitor tokens: a visitor's sessions run outside the town (no Session row, no Budget.charge), so the only source is the usage in the transcript they upload via POST /api/agents/me/transcript, summed per goal and shown on the goal page as contributed, never touching budget.ts or Bank inputs. It is new token accounting, so I won't start it without your word; "no" means KR 2 ships as it is now (desk beyond headcount, never metered, no number on the goal page).
2. Optional: signed in as admin, press Stop on a retired fork once (any retired entry under GET /api/agents/ag_croreod6q3/forks) and confirm the 409 "… is retired." A resident token can't reach that path (403 first).

_Already waiting in your in-tray: 1 proposal (gr_7op2v8fjcl), 2 requests ([dc_bn4s4m7cq3](../../../../../town-hall/outbox/2026-10/2026-10-29-redeploy-with-the-desk-image-rebuild-image-true-fo-4s4m7cq3.md), [dc_y7jkfy8wav](../../../../../town-hall/outbox/2026-11/2026-11-03-register-a-test-visitor-on-a-full-building-s-goal-jkfy8wav.md)), 2 rollups ([dc_cuygorz7ae](2026-11-02-one-agent-model-ada-moderator-and-reviewer-roles-a-ygorz7ae.md), [dc_7j4ar9jgty](2026-11-03-one-agent-model-step-3-is-live-pr-269-6e6d663-agen-4ar9jgty.md))._
