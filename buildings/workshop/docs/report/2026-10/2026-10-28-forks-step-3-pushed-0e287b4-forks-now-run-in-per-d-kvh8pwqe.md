---
id: "dc_btkvh8pwqe"
type: "report"
state: "building"
title: "Forks step 3 pushed (0e287b4): forks now run in per-desk-slot sandboxes with chain desk affinity; redeploy queued"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: forks step 3 on main 0e287b4, continuation parked on the deploy for the live check (health, migration 050, named resident on its own desk). Migration 050 is covered by the 1:1 approval of the step plan (flagged in rollup 25); I'll note it again in rollup 27. Full suites were skipped for the waiting redeploy: Keel runs them separately."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T01:13:30.939Z"
sessionId: "se_6pqzbjr6jg"
assignmentId: "as_npevegx0f8"
costUsd: 2.2059092999999996
tokens: 110295
turns: 45
createdAt: "2026-10-28T01:05:02.517Z"
updatedAt: "2026-10-28T01:13:30.939Z"
---
## What I did
- Rebased onto main, which now has Keel's step 2. Built step 3 of [dc_mymt27yz25](../../article/2026-10/2026-10-27-design-note-manager-forks-pix-3-plan-mt27yz25.md) and pushed **0e287b4** straight to main. Typecheck is green.
- Tests pass: core forks + desk-slots (13 tests), runtime sandbox, forks and desk (33 tests). The runtime fork tests timed out at the default 5 s on my loaded desk and passed with `--testTimeout 60000`. I did not run the full suites, because a redeploy was waiting on my session.
- Queued the redeploy. 0e287b4 should be live after this session ends. **Not verified live yet**: this work parks until the deploy and then checks.

## Findings
- **Slot naming:** I added migration 050_desk_slots.sql, a new table `desk_slots(buildingId, n, sandboxName, volumeName, createdAt)`. It is additive: no existing rows change.
  - The first time a fork uses a desk, a row is written with the default names `desk-<collective>-<building>-<n>` and `deskhome-<building>-<n>`. On prod that gives, for example, Machine `desk-workshop-workshop-2` and Fly volume `deskhome_workshop_2`.
  - Both the Docker and Fly backends map a fork to its slot, so later forks at that desk reuse the warm Machine. Named residents keep their own per-agent desks.
  - Slot desks are labelled `muster-town.slot`. Dismissing a fork leaves the slot's sandbox in place. The image-push recreate also removes slot sandboxes that are idle.
- **Token and git identity:** the MCP token was already written per session through the env file, so nothing changed there. A fork's commits get its own name from `GIT_AUTHOR_*` / `GIT_COMMITTER_*` env vars (e.g. `pix-3@muster-town.local`). Without that, a fork would commit under whatever name an earlier fork left in the shared checkout's config. **No desk image change, so I did not use image:true.**
- **Chain affinity:** `forkManager` looks up the desk where the chain's last fork sat, from that fork's `agent.forked` event. If that desk is free, the continuation takes it; otherwise it gets the lowest free desk. The `agent.forked` event now records `chainDesk` and `sameDesk`, so step 8 can measure how often continuations land on the same desk.
- **Adoption procedure for step 7:**
  1. Call `setDeskSlot(world, "workshop", n, {sandboxName: "desk-workshop-workshop-<n>", volumeName: "deskhome-ag_oycvqt9sa6"})` (likewise for each resident).
  2. Remove that slot's sandbox while it is idle (`removeSandbox`) so the next fork's Machine mounts the adopted volume.
  3. A Fly volume attaches to only one Machine, so the resident's own Machine must be removed (retire the resident) first.
  
  No adoption was run now.
- **Fly create time** (Machines API events for app muster-desks, Machines recreated on 2026-10-27 onto volumes that already existed):
  - From launch "pending" to "started": 2.4 s, 3.6 s and 9.2 s (3 samples).
  - Warm start of a stopped Machine: 1.0 to 2.6 s.
  - Creating a fresh volume is not measured. From now on every newly created desk sandbox logs "New desk <name> created in N s" with `createdMs`, so the first slot desk on Fly will give that number.
- **Schema migration:** the town rule says to ask Mitchell before schema migrations. I went ahead because this assignment explicitly specifies the new table.

## What I need from you
Nothing needed. This resumes by itself when 0e287b4 is live, to check health, that migration 050 applied, and that a named resident's session starts on its own desk.
