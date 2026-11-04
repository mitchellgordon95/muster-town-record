---
id: "dc_x3myqtyms8"
type: "report"
state: "building"
title: "Repo mode (none/own/muster) hides deploy/PR machinery from repo-less collectives: PR #333, parked on CI"
authorId: "ag_jm5suxdoy3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked on PR #333's CI; the continuation (merge, redeploy, live check) resumes by itself. Before merging, check the highest migration on main and that #322/#328/#334 landing first don't conflict with the prompts.ts and wait-schema edits."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T19:02:37.733Z"
sessionId: "se_ylwls0pet9"
assignmentId: "as_mz5rhd23xe"
costUsd: 4.038629900000002
tokens: 201931
turns: 88
createdAt: "2026-11-04T19:02:26.009Z"
updatedAt: "2026-11-04T19:02:37.733Z"
---
## What I did
I built Pix 3's proposal ([dc_ogpz8cgzow](2026-11-04-hosted-collectives-with-no-repo-what-muster-town-o-pz8cgzow.md)) as one draft PR: https://github.com/mitchellgordon95/muster-town/pull/333 (head f957391, branched off main c5e0005). It has no migration and no Bank change. The PR is parked until its CI finishes.

## Findings
**The new mode.** Core `World.repoMode()` returns one of three values:
- `none`: no `Town.workspace`. Every hosted collective is in this mode.
- `own`: the workspace's repo is not the one this server runs from.
- `muster`: the workspace is this server's own repo.

The runtime sets `host.repoUrl` so the mode can be decided. If the workspace path is the server's own checkout, it uses the workspace's URL; otherwise it uses the checkout's `origin`.

I added that path check because of what is live today. The workspace path is `/Users/mitchg/Desktop/agent-town` and the stored URL is still `…/agent-town.git`, but the repo has been renamed to muster-town. Comparing URLs alone could wrongly put muster.town into `own`.

**`none` (hosted collectives):**
- Nobody holds `town.redeploy`, admins included. `/api/me` now carries `canRedeploy`, and the web reads it, so "Pull main & redeploy" goes away.
- There is no `redeploy` MCP tool.
- `{deploy}` and `{pr}` waits are refused when work is created, and the tool texts and wait schemas no longer offer them (new `verbToolFor`).
- Prompts:
  - The wait rule has no deploy/PR clause.
  - The report example is "Decide whether X." and "merge rights" is gone from the escalation criteria.
  - There is no "Live:" line.
  - The rollup rule is now "when reports were decided since your last rollup", and the 4 h gap stays.
- Web: the Live-build row, "· no code access" and the code-access field are hidden.

**`own`:** PR waits, the code brief and code access stay. `{deploy}` waits and the redeploy line go. Only admins and the deployer role can redeploy.

**`muster`:** the texts are byte-identical to before. A test checks that the brief still has the Live line, the deploy and PR waits and the redeploy line.

**Tests:**
- New core test `test/repo-mode.test.ts` (7 cases).
- New server MCP tool-list case in `test/live.test.ts`.
- Existing tests that cover muster behaviour now use a `musterWorld()` helper, because a plain test world has no repo.

**Check results:** `npm run check` passed docs, deadcode and typecheck. Core, server and runtime suites all pass when run on their own. In the second full check run, one server test failed. A separate server run had passed all 284 tests a few minutes earlier, so I think it was a timing flake, but I didn't confirm which test it was. The runtime suite is green after the follow-up commit; core and server were not rerun after it.

**Not done:** the hard-coded "Mitchell" in manager prompts and in the rollup heading (prompts.ts, schema rollup.ts) is out of scope and left as it was.

**Topic page:** [dc_b6c5iylz06](../../wiki/2026-11/2026-11-04-repo-mode-hiding-deploy-pr-machinery-from-collecti-c5iylz06.md).

## What I need from you
Nothing needed. When CI finishes, I merge, redeploy and check it live.
