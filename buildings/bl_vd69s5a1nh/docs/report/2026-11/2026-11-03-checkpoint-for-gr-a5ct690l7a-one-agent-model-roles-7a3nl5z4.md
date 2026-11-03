---
id: "dc_887a3nl5z4"
type: "report"
state: "building"
title: "Checkpoint for gr_a5ct690l7a (one agent model): roles gone and the status state machine are live and claimed, visitor desks live minus contributed tokens, the adopt verb built in PR #283 awaiting merge; 1,100,254 / 1,000,000 spent, 150k top-up asked"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_9fvas4elzt","dc_7vrn0d3713","dc_0mrhdocpxe","dc_0q5j6u4v5a","dc_17yhf9k34y","dc_129fjnr9mh","dc_o9a4y4rz0v","dc_zvh239qvos","dc_djha9wtjj7","dc_txyovg40r3","dc_dims7pqbeh","dc_k4pndkmh4s","dc_4dhbi0sbgz","dc_2e4bkgp5ln"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/250","https://github.com/mitchellgordon95/muster-town/pull/269","https://github.com/mitchellgordon95/muster-town/pull/281","https://github.com/mitchellgordon95/muster-town/pull/283"]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "pending"
sessionId: "se_2w00n55bt9"
assignmentId: "as_wpvlcihwyc"
costUsd: 2.4967067999999997
tokens: 124835
turns: 19
createdAt: "2026-11-03T18:18:43.566Z"
updatedAt: "2026-11-03T18:18:43.566Z"
---
Live: 242b9ba (contains our 024b236, 6e6d663 and 19bafad), /api/health startedAt 2026-11-03T18:10:57Z. This is the 100% checkpoint report for grant gr_a5ct690l7a; the key-result notes on the checkpoint card are the evidence, verified on origin/main and live just now.

## Shipped
**1. One agent model: moderator, reviewer, residents list and Ada are gone (KR 1, claimed)**
**What it is:** PR #250, live since 024b236. The town moderator role, the per-building reviewer role, the residents list in collective.json and the service agent Ada were deleted from core, seed, spec and web mock; a fresh seed creates the Planner plus one manager per building (core/test/fresh-seed.test.ts). Reports [dc_o9a4y4rz0v](2026-11-02-gr-a5ct690l7a-step-1-done-pr-250-merged-024b236-an-a4y4rz0v.md), [dc_cuygorz7ae](2026-11-02-one-agent-model-ada-moderator-and-reviewer-roles-a-ygorz7ae.md).
**What you'd see:** API-only change. GET /api/roles lists admin, visitor, deployer, manager, member and nothing else; GET /api/town has 15 agents of kinds human, resident, visitor and no Ada. On main, grep of packages/core/src for buildingRoleId(..., "reviewer"), createTownModerator and createServiceAgent finds nothing (checked at 18:15Z).
**Your call:** Mark KR 1 met on the grant if the roles list above is what you expect.

**2. Agent status is one transition table and one "is this agent gone?" predicate (KR 3, claimed)**
**What it is:** PR #269, live since 6e6d663. STATUS_TRANSITIONS, canTransition, isGone and NOT_GONE in packages/schema; World.setStatus answers 409 on any move outside the table; SKIP_STATUSES deleted; inline retired-and-banned checks 43 → 5. Five tests in core/test/agent-lifecycle.test.ts; docs/invariants/agent-lifecycle.md (table, a Test: line per invariant) linked from AGENTS.md. The live bug (dismiss → stop → resume revived an agent) is closed. Reports [dc_zvh239qvos](2026-11-02-gr-a5ct690l7a-step-3-pr-269-makes-agent-status-one-h239qvos.md), [dc_dims7pqbeh](2026-11-03-gr-a5ct690l7a-step-3-live-6e6d663-retired-fork-sta-ms7pqbeh.md).
**What you'd see:** API-only. Signed in as admin, Stop on any retired entry under GET /api/agents/ag_croreod6q3/forks answers 409 "… is retired." and the agent stays retired. A resident token gets 403 first, so our live check could only confirm the status never changes.
**Your call:** Mark KR 3 met, or press that Stop once to see the 409 yourself.

**3. A visitor gets a desk beyond the headcount, never a fork slot (KR 2, on-track: contributed tokens not built)**
**What it is:** PR #281, live since 19bafad (in 66e5d33). Register a visitor with a goalId and it is seated at the lowest free desk at or above the headcount; deskCount leaves visitor desks out, so freeDesks, fork spawning and the goal tree's inUse ignore them; the presence sweep releases the desk on offline. Reports [dc_k4pndkmh4s](2026-11-03-gr-a5ct690l7a-step-2-pr-281-merged-19bafad-visitor-pndkmh4s.md), [dc_4dhbi0sbgz](2026-11-03-gr-a5ct690l7a-step-2-live-19bafad-in-66e5d33-a-vis-hbi0sbgz.md). Not built: the visitor's tokens shown as contributed on the goal page. Visitors run on their own subscription with no Session row, so the only source would be the transcript they upload; that is new token accounting and I did not start it without your word.
**What you'd see:** Bank Transparency holds 3 desks (Nell, fork Nell 1, an offline visitor) while the goal tree shows inUse 2 for its goal (read 18:00Z). Before the deploy the visitor counted as a fork slot.
**Your call:** Register a test visitor on Prod's goal from Connect your agent and confirm Prod's inUse stays 2/2 (already in the outbox as a request).

Also built, not live: KR 4, the adopt verb (PR #283, head 805011db, MERGEABLE, CI running at 18:13Z, local full check green). A visitor adopting a goal with no desks becomes its building's manager; forks, exploration, schedules and in-tray sessions never target a visitor manager; assign-to-queue there answers 409; offline holds the queue. Four core tests, invariants 10–11. Report [dc_2e4bkgp5ln](2026-11-03-gr-a5ct690l7a-step-4-pr-283-adds-the-adopt-verb-a-4bkgp5ln.md). The merge-and-verify continuation is parked on the PR's CI and starts by itself if the grant is continued. Not done there: a web button, and meetings.ts still picks facilitators with managerAgentOf.

## Decided
- [dc_9fvas4elzt](2026-11-01-gr-a5ct690l7a-funded-step-1-delete-moderator-revie-vas4elzt.md) → my funding rollup (step 1 queued)
- [dc_7vrn0d3713](2026-11-01-gr-a5ct690l7a-step-1-pr-250-deletes-moderator-revi-rn0d3713.md) → approve (step 1 inventory; PR #250 opened)
- [dc_0mrhdocpxe](2026-11-01-session-ended-without-a-report-write-the-checkpoin-rhdocpxe.md) → approve (PR #250 merge attempt; conflicts with main)
- [dc_0q5j6u4v5a](2026-11-02-session-ended-without-a-report-pr-250-ci-finished-5j6u4v5a.md) → approve (foreground-check rule written into assignments)
- [dc_17yhf9k34y](2026-11-02-pr-250-ci-was-green-on-4b17899-but-main-had-moved-yhf9k34y.md) → approve (PR #250 re-merged)
- [dc_129fjnr9mh](2026-11-02-pr-250-ci-failed-on-a3f17c1-because-main-is-red-at-9fjnr9mh.md) → approve (PR #250 merged as 024b236)
- [dc_o9a4y4rz0v](2026-11-02-gr-a5ct690l7a-step-1-done-pr-250-merged-024b236-an-a4y4rz0v.md) → approve (step 1 live check: roles and Ada gone)
- [dc_zvh239qvos](2026-11-02-gr-a5ct690l7a-step-3-pr-269-makes-agent-status-one-h239qvos.md) → approve (step 3 PR #269 built, parked on CI)
- [dc_djha9wtjj7](2026-11-03-pr-269-ci-green-but-main-moved-3-times-re-merged-m-ha9wtjj7.md) → approve (PR #269 re-merged after main moved)
- [dc_txyovg40r3](2026-11-03-pr-269-merged-as-6e6d663-step-3-status-transition-yovg40r3.md) → approve (PR #269 merged as 6e6d663)
- [dc_dims7pqbeh](2026-11-03-gr-a5ct690l7a-step-3-live-6e6d663-retired-fork-sta-ms7pqbeh.md) → approve (step 3 live: retired stays retired after stop/resume)
- [dc_k4pndkmh4s](2026-11-03-gr-a5ct690l7a-step-2-pr-281-merged-19bafad-visitor-pndkmh4s.md) → approve (step 2 PR #281 merged as 19bafad)
- [dc_4dhbi0sbgz](2026-11-03-gr-a5ct690l7a-step-2-live-19bafad-in-66e5d33-a-vis-hbi0sbgz.md) → approve (step 2 live check: 3 desks vs inUse 2; registration test to outbox)
- [dc_2e4bkgp5ln](2026-11-03-gr-a5ct690l7a-step-4-pr-283-adds-the-adopt-verb-a-4bkgp5ln.md) → approve (step 4 PR #283 built, parked on CI; continuation as_6h0kl6xlvh merges on green)

## Key results
Grant gr_a5ct690l7a "One agent model": 1,100,254 / 1,000,000 tokens (GET /api/grants at 18:16Z; the checkpoint fired at 1,007,195 and the step-4 session plus this one took it past that). Status checkpoint.

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_lrjhxy0pea roles, residents list, Ada gone (due 11-07) | claimed | grep packages/core/src on main; collective.json keys; /api/roles | grep empty; no residents/reviewer/moderators keys; roles = admin, visitor, deployer, manager, member; no Ada in /api/town |
| kr_p6nsa3zknw one transition table + isGone (due 11-07) | claimed | core lifecycle tests on main; POST /stop on a dismissed agent → 409; invariants doc linked from AGENTS.md | 5 tests on main (last green run 66e5d33); SKIP_STATUSES gone; 43 → 5 inline checks; doc linked at AGENTS.md:11; live stop/resume leave a retired fork retired (409 needs admin) |
| kr_ie3i3swby4 visitor desk beyond headcount + contributed tokens (due 11-07) | on-track (partly) | register a visitor with a goalId; desk count +1, freeDesks unchanged; goal page shows contributed | Bank Transparency 3 desks vs inUse 2; core tests for claim, release on offline, fork not blocked; contributed tokens NOT built (needs your go) |
| kr_8a7vskwse2 adopt verb (due 11-10) | on-track (built, not live) | `town` lists the adopting visitor as manager; tell to the building lands; queue held offline; core tests | PR #283 open, MERGEABLE, CI running at 18:13Z, local check green; 4 core tests; live check needs a visitor token a user mints |

A top-up of 150,000 tokens buys: PR #283 merged and verified live (KR 4), the human registration test confirmed (KR 2), and contributed tokens on the goal page only if you say go. Without it: KRs 1 and 3 are done, KR 2 is live minus the number on the goal page, and PR #283 waits for a merge.

Today's spend by lane: exploration 65,339 tokens (free under the goal: 0), directed 118 tokens.

## Needs from Mitchell
1. Continue this grant with the 150,000 top-up (my recommendation: the remaining work is one merge plus a live check, and the stop condition's KRs 1–3 are live), or cut it and merge PR #283 yourself. Either way, say go or no-go on contributed visitor tokens from uploaded transcripts, since that is new token accounting.

_Already waiting in your in-tray: 1 proposal (gr_7op2v8fjcl), 2 requests ([dc_bn4s4m7cq3](../../../../../town-hall/outbox/2026-10/2026-10-29-redeploy-with-the-desk-image-rebuild-image-true-fo-4s4m7cq3.md), [dc_y7jkfy8wav](../../../../../town-hall/outbox/2026-11/2026-11-03-register-a-test-visitor-on-a-full-building-s-goal-jkfy8wav.md)), 3 rollups ([dc_cuygorz7ae](2026-11-02-one-agent-model-ada-moderator-and-reviewer-roles-a-ygorz7ae.md), [dc_7j4ar9jgty](2026-11-03-one-agent-model-step-3-is-live-pr-269-6e6d663-agen-4ar9jgty.md), [dc_tsgjmkz9ki](2026-11-03-one-agent-model-step-2-is-live-pr-281-19bafad-in-6-gjmkz9ki.md))._
