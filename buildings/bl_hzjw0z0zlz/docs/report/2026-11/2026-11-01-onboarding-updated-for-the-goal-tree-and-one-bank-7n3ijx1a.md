---
id: "dc_g77n3ijx1a"
type: "report"
state: "building"
title: "Onboarding updated for the goal tree and one Bank (3e3cbdd + 08c16a7 on main); live check parked on deploy"
authorId: "ag_4aklioi31g"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. 3e3cbdd + 08c16a7 on main; live check already queued as as_kfwhihp319 (waits on deploy 08c16a7). Gap 1 (placeholder Fund/Join/Trust goals in every new collective) goes to Mitchell in the next rollup's Needs; gaps 2–7 (Workshop/core strings) relayed to Pix by tell."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-01T02:08:16.970Z"
sessionId: "se_m4o1f4hasj"
assignmentId: "as_zv1dq0j65j"
costUsd: 3.1090252
tokens: 155451
turns: 68
createdAt: "2026-11-01T02:07:54.239Z"
updatedAt: "2026-11-01T02:08:16.970Z"
---
## What I did
Read the design doc (docs/how-work-gets-done.md, written 2026-10-31) and checked it against main and the live server. Rewrote the onboarding copy that still described the old model, pushed **3e3cbdd** and **08c16a7** straight to main, and parked a live check on the deploy of 08c16a7. When I checked, the live server was on d9f28c5 (health 2026-11-01T02:00:09Z).

## Findings
**What landed.** The refactor is on main and live: PRs #169, #173, #171, #168 and #179, migrations 067–070. That covers one Bank balance with earmarks, free tokens per goal, the explore tick (100k chunks, no allowance), grants that carry their own key results (goals keep none), map shapes, desks −/+ on the goal canvas (193e19c) and an operating reserve (0ffd323). Two things came after I started: since 4578ded the root goal always has a captain (migration 078), and the Dashboard was removed (7ad702d). The doc is ahead of the code only on step 6 (recurring grants for standing duties), which still waits on Mitchell's q2. The manual had already been partly updated by the Workshop's docs sweep (5cf58a3).

**What changed (all of it is Onboarding's code):**
- **Manual** (1,891 of the 1,900-word cap, which `npm run check:docs` now enforces):
  - "What Muster Town is" now explains the goal tree: each building is attached to one goal, a building's desks are how many forks work at once, and captains get grant proposals, checkpoints and rollups in their **Mine** list. A goal without its own captain rolls up to the nearest captain above it.
  - Funding: the Donate form's **Earmark for** field; one balance with no per-building budgets; how free tokens are added up.
  - Running a collective: the goal tree tools and desks −/+. "Daily budget" is gone, because `dailyTokensPerAgent` is no longer read anywhere.
  - Start your own collective: **First steps, in order** — goals, then a building attached to one, then a key at the Bank.
  - Other sections trimmed to stay under the cap.
- **README**:
  - A collective is one goal tree.
  - Step 5 builds goals first, then buildings and desks.
  - Grants carry their own key results.
  - Removed the "add a key result in the Goals tab / blocked: no key results" step.
  - `dailyTokensPerAgent` is marked as read by nothing.
  - Donations go to the Bank.
- **docs/hosted-collectives.md**: "First building" now starts from the goal tree.
- **In-town overlay** (HowItWorks.tsx:26): "Sign in with GitHub, then ask to join". The live JS still had "…to talk and review", which contradicts the honest guest card from kr_a32db87f39.
- **Homepage** (home.ts:109): "Fund a goal. Back one goal a collective is working toward; your money pays only for work under it."
- Tests: typecheck passes, web 213/213, server 253/253, core manual-seed passes, check:docs OK. I did **not** take mock screenshots of the one-line overlay change; the live check will screenshot it.

**Onboarding paths as a stranger walks them:**
- (a) **A new collective** now has written guidance to create goals first, then buildings, then desks (manual, README, hosted doc). But the empty collective doesn't match it: a fresh database's tree is the root plus Muster Town's own "Fund", "Join" and "Trust" placeholder goals. I confirmed this with a fresh `seededWorld` in a test.
- (b) **A new member** can now read in the manual's first section how goals, buildings, desks, the Bank and captains fit together. The first screens (homepage, overlay) still don't mention the tree, which is deliberate: the style guide keeps insider words off first screens.

**Gaps in core and Workshop code (for Mitchell; I did not change these):**
1. `packages/core/migrations/061_goal_tree.sql:36-39`: every new collective, hosted or self-hosted, starts with placeholder goals "Fund", "Join" and "Trust" under its root. Separately, the root's text is set to "The town goal" when the table is created, and `Goals.ensure` (goals.ts:504-506) only writes the text when the root is missing. I infer from the code, but have not run a hosted create to confirm, that a new hosted collective's root reads "The town goal" rather than its founder's goal.
2. `packages/web/src/panels/GoalTreePanel.tsx:208`: the empty state says "add a dated one with + Key result", but that button is gone (step 5).
3. `packages/web/src/panels/PlanningPanel.tsx:53`: the New building goal hint says "its work names open key results under it". That is no longer true; work names a goal or a grant.
4. `packages/web/src/panels/BuildingPanel.tsx:207`: the desks hint says it "sets the daily cap (the collective's daily budget / agent × desks)", but the daily caps were removed.
5. `packages/web/src/panels/GoalsTab.tsx:57` still shows a building-level "Objectives and key results" editor. Also still present: "Blocked: no key results" in `keyResults.ts:40` and `Places.tsx:168`, and a blocked deck slide in `core/src/review-deck.ts:212-218` that says "Write its key results (Building → Settings)". These contradict §4 of the design doc.
6. `docs/goals.md:41`: the node-detail toolbar still lists "+ Key result".
7. `GoalTreePanel.tsx:238` (Change this goal hint) and `:452` (Retire) still talk about a goal's "open key results".

**Still stale on Onboarding's side:** nothing I know of. Whether the live manual takes the new edition depends on its seeded tag; the live check verifies that.

## What I need from you
Decide whether a new collective should start without the Fund / Join / Trust placeholder goals (core, gap 1).
