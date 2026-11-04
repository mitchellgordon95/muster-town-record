---
id: "dc_tbendzyq71"
type: "report"
state: "building"
title: "Repo mode is live on 4815e19: muster.town keeps redeploy and its deploy/PR waits; hosted hollyville and trauma report \"none\""
authorId: "ag_48ac62qh1m"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Live check of repo mode on 4815e19 done: muster.town keeps redeploy and {deploy}/{pr}; hollyville and trauma report repoMode none and are gated. Goes into rollup 47 as the \"actual state\" Mitchell asked for. The hard-coded \"Mitchell\" follow-up is queued separately."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T19:36:40.592Z"
sessionId: "se_l97q5leg8r"
assignmentId: "as_vydbl43og5"
costUsd: 0.9588981
tokens: 47945
turns: 31
createdAt: "2026-11-04T19:36:25.822Z"
updatedAt: "2026-11-04T19:36:40.592Z"
---
## What I did
I confirmed the live build first. /api/health was read at 19:34:01Z and reported commit 4815e19, with the server started at 19:33:46Z. Then I checked muster.town and both hosted collectives read-only, over the WebSocket snapshot, MCP tools/list, building stats and the deployed web bundle. I also ran the tests that cover the deployed code on my desk. I did not redeploy, and the code needed no change. Topic page [dc_b6c5iylz06](../../wiki/2026-11/2026-11-04-repo-mode-hiding-deploy-pr-machinery-from-collecti-c5iylz06.md) is rewritten with the verified state.

## Findings
- **Mitchell's question, answered from live data.** Only two hosted collectives exist, /hollyville/ and /trauma/. Both report `repoMode: "none"` and have no workspace. Neither has started yet, so no agents have run in either. muster.town reports `muster` and its workspace is agent-town.git.
- **muster.town did not regress:**
  - The live MCP tools/list (35 tools) still has `redeploy`.
  - `submit_report.resumeWhen` and `assign.waitFor` still accept `{deploy}` and `{pr}`.
  - Workshop stats show host.commit 4815e19, which is what the Live-build row displays.
  - The manager brief's Live line is printed only in muster mode (`packages/core/src/prompts.ts:336`). The live mode is muster, and the test "muster: the Workshop's brief is as today" passes.
- **Hosted collectives are gated:**
  - Nobody holds `town.redeploy` in a hosted World, admins included (`packages/core/src/permissions.ts:66`). That makes `/api/me.canRedeploy` false (`packages/server/src/routes/town.ts:96`).
  - The "Pull main & redeploy" button shows only for holders of `town.redeploy` (`packages/web/src/panels/PlanningPanel.tsx:156`).
  - The Live-build row is hidden outside muster (`PlanSideBar.tsx:91`). The deployed bundle main-BtebppHd.js contains this gate.
  - The MCP server leaves out `redeploy` outside muster (`packages/server/src/mcp.ts:24`).
  - `validateWait` refuses `{deploy}` and `{pr}` when the mode is none (`packages/core/src/waits.ts:20`).
- **Tests:** core repo-mode + waits passed 17/17, and server live + redeploy passed 12/12. They include a repo-less world that gets no `redeploy` tool.
- **Not checked live:** I couldn't call `/api/me` on a hosted collective because it needs a user token there. I couldn't get a hosted agent's tool list because no agents have run there yet. Both are covered by the code paths and tests above.
- **Still open, outside this assignment:** "Mitchell" is hard-coded in the manager prompts and in the rollup heading, which is wrong for a hosted collective's captain.
- No leaks found.

## What I need from you
Nothing needed.
