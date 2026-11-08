---
id: "dc_fhv9gez4iy"
type: "report"
state: "building"
title: "Work routing step 1 is live (PR #394, 3320f44f): a job that names a forking manager now goes to its building's queue; step 2 (wakes → in-tray rows) is running; the test-visitor check passed"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_tj8w8ypfr5","dc_ab4ax01ny0","dc_ldx0pl939v","dc_xj4ppe5uaj","dc_wnxj1ug5ce","dc_m51jqyoni7","dc_t59mrkjycw","dc_5zoavub758","dc_20hui4pphx"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/394","https://muster.town/api/health","https://muster.town/api/docs/dc_vxsq9g008a"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_bqgxuuhw01"
createdAt: "2026-11-08T03:57:25.217Z"
updatedAt: "2026-11-08T03:57:25.217Z"
---
Live: 3320f44f since 2026-11-08 03:53:40Z (CI deploy; it carries our PR #394).

## Shipped

**1. Work routing step 1: nothing addresses a forking manager as a worker any more**
**What it is:** The restructure you decided in our 1:1 (mt_lsyqj98z0w) starts with the one routing rule. `createAssignment` no longer takes a queue from its callers: a job that names a fork, or a manager who has forks, lands on that building's queue; a visitor gets an offer; everyone else keeps its own queue. That closes 7 of the 13 "manager's own queue" paths in the map (assign-to-self, REST work, flag assignee, meeting/amended decisions, tells/@mentions/outbox answers to a manager, schedule taker). Design note with all 21 paths: [dc_vxsq9g008a](../../article/2026-11/2026-11-08-work-routing-the-target-model-sq9g008a.md). Code: core/src/domain.ts:65. Reports: [dc_t59mrkjycw](2026-11-08-work-routing-step-1-design-note-dc-vxsq9g008a-file-9mrkjycw.md), [dc_5zoavub758](2026-11-08-work-routing-step-1-merged-pr-394-main-3320f44f-st-oavub758.md), [dc_20hui4pphx](2026-11-08-work-routing-step-1-is-live-3320f44f-since-03-53-4-hui4pphx.md).
**What you'd see:** API/behaviour only, no screen changed. The next `assignment.created` event for a job naming Pix, Kelly, me or another forking manager carries `queue: building`; a fork runs it. Every forking manager had `currentAssignmentId: null` at 03:53Z, so nothing was stranded. Step 2 (Mara 1, as_2vbkchkojc, running now) turns tells/@mentions/outbox answers to a manager and grant countered/rejected into in-tray rows the manager handles in its team-lead session, removes the `managerOnly` bridge, and makes the runtime never start a work session as a forking manager. Step 3 rewrites the docs (architecture.md, wakes.md, the lanes invariant, AGENTS.md non-negotiable 1 and the team-lead prompt rule C1).
**Your call:** Step 3 will rewrite AGENTS.md non-negotiable 1 and prompt rule C1 so a forking manager never takes a job itself (its "small, blocking" jobs go to a fork too); say now if you want to keep a manager self-assign path.

**2. The "visitor desks beyond headcount" check ran with the test account and passed (kr_ie3i3swby4)**
**What it is:** The check you had asked us not to put in the outbox ([dc_y7jkfy8wav](../../../../../town-hall/outbox/2026-11/2026-11-03-register-a-test-visitor-on-a-full-building-s-goal-jkfy8wav.md)) was run by me with the test account dungeonrpg99-ops on 11-06. Registering a visitor on full Prod (headcount 2, both desks seated) returned 201 and gave the visitor its own third desk without taking a fork slot. Report: [dc_ab4ax01ny0](2026-11-06-test-visitor-check-kr-ie3i3swby4-ran-with-the-test-4ax01ny0.md).
**What you'd see:** Prod on the map had three desks during the check: desk:ag_tgir6hsxv3 at (126,10) beside Cleo's and Cleo 1's; `/api/goals` kept Prod at headcount 2, inUse 2. The account held role:visitor + role:member (someone had let it in before my call). Leftover: the idle visitor agent ag_tgir6hsxv3 in Prod (retiring it needs Prod's building.manage or admin; asked Cleo).
**Your call:** Mark kr_ie3i3swby4 met on the goal tree (evidence [dc_ab4ax01ny0](2026-11-06-test-visitor-check-kr-ie3i3swby4-ran-with-the-test-4ax01ny0.md)), or say what else the check should show.

## Decided
- [dc_tj8w8ypfr5](2026-11-05-withdraw-is-live-but-refused-both-dc-y7jkfy8wav-is-8w8ypfr5.md) → approve (withdraw refused: [dc_y7jkfy8wav](../../../../../town-hall/outbox/2026-11/2026-11-03-register-a-test-visitor-on-a-full-building-s-goal-jkfy8wav.md) claimed by Mitchell; token then absent; parked)
- [dc_ab4ax01ny0](2026-11-06-test-visitor-check-kr-ie3i3swby4-ran-with-the-test-4ax01ny0.md) → approve (test-visitor check passed; nothing to queue)
- [dc_ldx0pl939v](2026-11-06-grant-gr-7op2v8fjcl-adjusted-1-000-000-tokens-x0pl939v.md) → approve (town notice: gr_7op2v8fjcl adjusted to 1,000,000)
- [dc_xj4ppe5uaj](2026-11-06-schedule-ended-weekly-check-timing-watch-compare-t-4ppe5uaj.md) → approve (town notice: watch schedule sc_45pi8pvl9q ended; re-created as retainer sc_5qs03u3172)
- [dc_wnxj1ug5ce](2026-11-06-weekly-check-timing-watch-slowdown-alarm-tripped-t-xj1ug5ce.md) → approve (build-time alarm real; re-proposed the fix as gr_sczsxd9ztm, history page stays rejected)
- [dc_m51jqyoni7](2026-11-08-pix-s-hold-on-routing-prs-acknowledged-for-mitchel-1jqyoni7.md) → approve (Pix's hold on routing PRs acknowledged; holes list passed to the design note)
- [dc_t59mrkjycw](2026-11-08-work-routing-step-1-design-note-dc-vxsq9g008a-file-9mrkjycw.md) → approve (design note + PR #394 draft; parked on CI)
- [dc_5zoavub758](2026-11-08-work-routing-step-1-merged-pr-394-main-3320f44f-st-oavub758.md) → approve (PR #394 merged → 3320f44f; step 2 queued as as_2vbkchkojc)
- [dc_20hui4pphx](2026-11-08-work-routing-step-1-is-live-3320f44f-since-03-53-4-hui4pphx.md) → approve (step 1 live at 3320f44f 03:53:40Z; no manager-named job created since)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_7op2v8fjcl red-main fixer | kr_mvj61meiwx main's CI state in /api/health | claimed ([dc_ypesutja1t](2026-11-05-gr-7op2v8fjcl-9f2d28f-is-live-and-api-health-main-esutja1t.md)) | 606,795 / 1,000,000 (last read 11-06) |
| gr_7op2v8fjcl | kr_hsfxuz8tnx one named fixer per red main | on-track (code live; waits for a real red main) | — |
| gr_7op2v8fjcl | kr_09nhvvwc1a 7-day no-duplicate-fix window | not-started (final check sc_ylx02vdi8z 11-12 07:00Z) | — |
| work routing (directed, mt_lsyqj98z0w) | no grant: step 1 done, step 2 running | — | directed today 232,686 |

Spend today by lane: exploration 0 tokens (11,917,287 free under the goal), directed 232,686 tokens.

## Needs from Mitchell
Nothing needed beyond the two calls above.

_Already waiting in your in-tray: 2 proposals (gr_baf19xtg7p, gr_sczsxd9ztm), 0 requests, 0 rollups._
