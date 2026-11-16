---
id: "dc_f5vs6hubmx"
type: "report"
state: "building"
title: "repoMode fix in draft PR #481 (migration 118); parked on its CI"
authorId: "ag_j2dkq8sex4"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The parked continuation (as_ex3l7ndp82, waiting on PR #481's CI) merges it if green; nothing else queued. Note for the pin grant gr_y4s2j99vgm: its step 1 must take migration 119, not 118."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-16T19:41:20.210Z"
sessionId: "se_83xvmcewq9"
assignmentId: "as_ct19vgpj00"
costUsd: 0.9839532000000002
tokens: 49198
turns: 23
createdAt: "2026-11-16T19:41:07.163Z"
updatedAt: "2026-11-16T19:41:20.210Z"
---
## What I did
I found where the stale URL lives and wrote migration 118 to rewrite it. I added a test, a docs note and a log.d entry, and ran `npm run check` (green). Then I pushed and opened draft PR #481: https://github.com/mitchellgordon95/muster-town/pull/481 (commit 8d14960a).

## Findings
- **Where the URL is stored.** `Town.workspace` sits in `meta` key 'town'. It is written only by `seedDefaults` (core/src/seed.ts:141-147, :213-214) from collectives/workshop/collective.json, which gives no repoUrl. `withRepoUrl` then fills it from the checkout's origin once and never rewrites it. No admin endpoint sets it. So the stored value `git@github.com:mitchellgordon95/agent-town.git` is left over from before the rename. The runtime's ws.path shortcut (runtime/src/index.ts:886-889) does not apply on the server, because the stored path is a laptop path.
- **The fix.** `packages/core/migrations/118_workspace_repo_renamed.sql` changes `mitchellgordon95/agent-town` to `mitchellgordon95/muster-town` inside the stored repoUrl and keeps the URL's form. Other repos are left alone. After it runs, `repoKey` matches the host origin, so `repoMode` is "muster" again. Managers and forks get `town.redeploy` back, along with the redeploy tool, `{deploy}` waits, the live line and the live build in PlanSideBar.
- **Tests.** New file core/test/workspace-repo-renamed-migration.test.ts covers both URL forms (each now matches the host origin) and checks that another owner's agent-town and a workspace with no URL are not changed. The repo-mode.test.ts fixtures now use the new name. `npm run check`: docs 1s, deadcode 10s, typecheck 43s, tests 7m21s (88 files, 432 tests passed).
- **Side effect.** `repoNameOf` now returns muster-town, so desks will clone the repo again into `/home/agent/work/muster-town` on their next session. Old agent-town checkouts stay on disk but are no longer used.
- **Migration number.** 118 is also the number the proposed pin grant gr_y4s2j99vgm planned for its step 1. That step must take 119.
- **Nothing is live yet.** This changes nothing until a redeploy runs. That needs either Mitchell pressing redeploy (ask ak_nugzl9rheu) or CI's deploy token being restored (ask ak_tlets696sj). I did not call redeploy.

## What I need from you
Nothing needed. I resume when PR #481's CI finishes, and merge it if it is green.
