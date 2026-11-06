---
id: "dc_cuygorz7ae"
type: "report"
state: "building"
title: "One agent model: Ada, moderator and reviewer roles are gone live (PR #250); the status state machine (PR #269) is in CI"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_o9a4y4rz0v","dc_zvh239qvos","dc_dbrkeiac5r","dc_eu63i51a65","dc_17yhf9k34y","dc_129fjnr9mh"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"1:1: Mitchell and Secretary\": No-go on visitor token accounting for gr_a5ct690l7a KR 2 (Mitchell, 1:1 mt_i50xwu4z2t at 18:16 UTC: \"i don't think we need to worry about accounting for visitor"
decidedBy: "ag_7tiwyqva83"
decidedAt: "2026-11-04T18:17:13.627Z"
sessionId: "se_0str0nvnlf"
createdAt: "2026-11-02T18:21:50.682Z"
updatedAt: "2026-11-04T18:17:13.627Z"
---
Live: 7f081f7 (Teo's). Ours live since 024b236 at 2026-11-02T03:30:34Z.

## Shipped
**1. One agent model, step 1: the town moderator role, the building reviewer role, the residents list and Ada are gone**
**What it is:** Grant gr_a5ct690l7a, KR kr_lrjhxy0pea. PR #250 (merged as 024b236) deletes createTownModerator, the per-building reviewer role and its facilitator fallback, the residents/reviewer/moderators keys in collectives/*.json (a building now names one manager with explicit headcount), and Ada (kind service). A role migration drops the dead roles and memberships on open. Fresh seed = Planner plus one manager per building. It also fixed main's red deadcode check (4 unused exports from another building). Reports [dc_o9a4y4rz0v](2026-11-02-gr-a5ct690l7a-step-1-done-pr-250-merged-024b236-an-a4y4rz0v.md), [dc_eu63i51a65](2026-11-02-gr-a5ct690l7a-step-1-finish-pr-250-merged-with-mai-63i51a65.md), [dc_17yhf9k34y](2026-11-02-pr-250-ci-was-green-on-4b17899-but-main-had-moved-yhf9k34y.md), [dc_129fjnr9mh](2026-11-02-pr-250-ci-failed-on-a3f17c1-because-main-is-red-at-9fjnr9mh.md).
**What you'd see:** API-only. /api/town lists no Ada and no agent of kind service; /api/roles has only admin, visitor, member, deployer plus manager/member per building (no moderator, no reviewer); all 8 buildings keep their manager. On main, grep packages/core/src for buildingRoleId(…, "reviewer"), createTownModerator and createServiceAgent finds nothing (I re-checked on the 70d90b7 snapshot: 0 hits).
**Your call:** Mark kr_lrjhxy0pea met on the grant if the live checks above satisfy you.

In CI, not yet live: step 3 (KR kr_p6nsa3zknw), PR #269 by Mara 1 ([dc_zvh239qvos](2026-11-02-gr-a5ct690l7a-step-3-pr-269-makes-agent-status-one-h239qvos.md)). Agent status becomes one transition table (STATUS_TRANSITIONS in schema, enforced in World.setStatus with a 409 on illegal moves), one isGone predicate replaces the inline retired/banned checks (43 lines → 5), SKIP_STATUSES in the budget sweep goes, and stopAgent refuses a retired or banned agent, so dismiss → stop → resume no longer revives it. 5 named tests plus docs/invariants/agent-lifecycle.md. Local check green; a fork merges it on green CI and verifies live.

## Decided
- [dc_o9a4y4rz0v](2026-11-02-gr-a5ct690l7a-step-1-done-pr-250-merged-024b236-an-a4y4rz0v.md) → approve (step 1 done and live; step 3 queued)
- [dc_zvh239qvos](2026-11-02-gr-a5ct690l7a-step-3-pr-269-makes-agent-status-one-h239qvos.md) → approve (step 3 built, parked on PR #269 CI; continuation as_i7b6buocg2 merges and verifies live)
- [dc_eu63i51a65](2026-11-02-gr-a5ct690l7a-step-1-finish-pr-250-merged-with-mai-63i51a65.md) → approve (PR #250 conflicts resolved, parked on CI)
- [dc_17yhf9k34y](2026-11-02-pr-250-ci-was-green-on-4b17899-but-main-had-moved-yhf9k34y.md) → approve (re-merged main, manual trimmed under its word cap)
- [dc_129fjnr9mh](2026-11-02-pr-250-ci-failed-on-a3f17c1-because-main-is-red-at-9fjnr9mh.md) → approve (fixed main's red deadcode check on the branch)
- [dc_dbrkeiac5r](2026-11-02-gr-wkimo647v2-rejected-no-note-nothing-follows-now-rkeiac5r.md) → approve (gr_wkimo647v2 rejected without a note; PR #247 kept as a parked draft)

## Key results
Grant gr_a5ct690l7a "One agent model" (funded 1,000,000; spent 631,112):

| Key result | Status | Evidence |
|---|---|---|
| kr_lrjhxy0pea moderator, reviewer, residents list, Ada gone (due 11-07) | at-risk in the town; work live since 024b236 | /api/town no Ada, /api/roles no moderator/reviewer, greps 0 on main |
| kr_p6nsa3zknw status transition table + isGone + stop guard (due 11-07) | not-started in the town; PR #269 in CI | core tests named in the KR pass locally; live 409 check after merge |
| kr_ie3i3swby4 visitor desk beyond headcount (due 11-07) | not-started | queued after step 3 is live |
| kr_8a7vskwse2 adopt verb for a goal with no desks (due 11-10) | not-started | last; may become a follow-up grant per the stop condition |

Today's spend by lane: exploration 0 tokens (free under the goal: 0), directed 147,269 tokens.

## Needs from Mitchell
- Build-time fixes: after gr_wkimo647v2 was rejected, PR #247 (one file, the check-timing fix) sits as a draft and the weekly timing watch fires next in about 3.5 days. Should I merge PR #247 on its own, or wait for the watch to alarm?

_Already waiting in your in-tray: 0 proposals, 1 request (dc_bn4s4m7cq3), 0 rollups._
