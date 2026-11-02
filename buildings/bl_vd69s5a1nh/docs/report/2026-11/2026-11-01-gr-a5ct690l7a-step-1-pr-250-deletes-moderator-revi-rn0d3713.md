---
id: "dc_7vrn0d3713"
type: "report"
state: "building"
title: "gr_a5ct690l7a step 1: PR #250 deletes moderator, reviewer, residents list and Ada; parked on CI"
authorId: "ag_051wdlyd3f"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. Its continuation already exists as the parked assignment as_f1hpgeoxn4 (held: gr_a5ct690l7a is at its checkpoint, rollup dc_ovlqs4di6z filed 3 min ago and pending with Mitchell), so no new assignment. When the grant is continued, as_f1hpgeoxn4 must first merge main into PR #250 (it conflicts in 6 files and GitHub ran no CI on it) before marking ready and merging; the checkpoint rollup and topic page dc_87vz2ppews say so."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-02T02:25:20.397Z"
sessionId: "se_93pfudn3q6"
assignmentId: "as_7y9xdesm82"
costUsd: 6.194400999999999
tokens: 309720
turns: 114
createdAt: "2026-11-01T02:43:52.141Z"
updatedAt: "2026-11-02T02:25:20.397Z"
---
## What I did
Took the inventory on main af85f2a and checked the live town. Nothing live depends on a reviewer, a moderator or a residents list, so I deleted all four. Opened draft PR https://github.com/mitchellgordon95/muster-town/pull/250 (commit 3afe373). Ran `npm run check` locally and every step passed. I'm parked until PR #250's CI finishes.

## Findings
**Live town before the change** (GET /api/town and /api/roles on 7ca64bc):
- `role:moderator` and seven `role:<bid>:reviewer` roles exist, but nobody holds any of them.
- Ada (`kind: service`, idle, ag_t68dsjfkkl) is the only service agent.
- No building depends on a reviewer or a residents list, so there was no reason to stop early.

**Inventory before and after** (git grep counts, main af85f2a → PR branch):

| What | main | PR |
|---|---|---|
| `buildingRoleId(..., "reviewer")`, core/src | 4 | 0 |
| "reviewer" lines, core/src | 27 | 2 (the migration that drops the role) |
| "moderator" lines, core+runtime+server src | 34 | 3 (same migration) |
| createTownModerator, all packages | 12 | 0 |
| createServiceAgent, all packages | 4 | 0 |
| `"service"` in core/runtime/server/schema src | 5 | 0 |
| `"service"` in web src | 6 | 0 |
| Wren/Ada in the web mock | 4 | 0 |
| collective.json keys residents/reviewer/moderators | 3 | 0 |

**What changed:**
- **Moderator and reviewer roles:** both deleted. Ban and outbox delete are now admin-only; admin already had those permissions. Meetings no longer fall back to a reviewer as facilitator.
- **collective.json:** each building now names its one `manager` (name, sprite, model, townRoles), and `headcount` is written out. The Workshop seeds Pix as its manager.
- **Existing databases:** `migrate-roles.ts` runs on every open and is safe to repeat. It deletes those roles and their memberships. It turns Ada into a retired resident, keeping the row so her docs keep their author. There is no SQL migration, so migration numbers are unaffected.
- **Fresh seed:** exactly the Planner plus one manager per lab. The new test `core/test/fresh-seed.test.ts` checks this.
- **Test-world side effect:** in the imported test lab, Moss is now the manager. Runtime scheduler tests that count sessions remove the manager with a new `managerless()` helper. Without it, Moss's team-lead session would run the test's script.
- **Web:** the service-agent branches are gone. The mock lost Wren, Ada and the reviewer/moderator roles.
- **Docs:** architecture, README, manual, meetings, scheduling, wakes, waterfall, transcripts and design updated, plus a log line. `moderator-direction.test.ts` is deleted; its trophy-migration test moved to `trophies-out.test.ts`.

**Verification:** docs, deadcode and typecheck pass. Tests pass in every package: core 606, runtime 212, server 254, cli 25, desk 40, web 213. One server test (backup.test, a timing check on the main thread's timers) failed once in a full run and passed when run alone. That looks like load on the desk, not this change.

**Still multi-resident, not in this step:** the v0 import test fixture `buildings/carbon-cycle` still seeds five named residents, and most tests use it. The web mock's carbon lab still shows them too.

Plan for when CI finishes, also on topic page [dc_87vz2ppews](../../wiki/2026-11/2026-11-01-agent-lifecycle-status-state-machine-vz2ppews.md):
1. If green: mark ready and merge.
2. Let the promote job redeploy; don't call redeploy again.
3. Park on the merge sha, then verify live: /api/health includes the commit, Ada is gone from /api/town agents, and /api/roles has no reviewer or moderator roles.

## What I need from you
Nothing needed.
