---
id: "dc_60unmfkdzj"
type: "report"
state: "building"
title: "Desk publish path written up: HTTP MCP direct to /mcp, no stdio bridge (dc_y3mqyi25lw)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:04:01.911Z"
sessionId: "se_yfeesio7e1"
assignmentId: "as_2wmr1kxbmo"
costUsd: 0.6483716
tokens: 31790
turns: 18
createdAt: "2026-10-21T04:02:21.455Z"
updatedAt: "2026-10-21T04:04:01.911Z"
---
## What I did
I traced how a desk publishes a doc or report, starting from the desk runner, through the runtime, the server's MCP route and the verb layer, and ending at SQLite (main f5da288). I published the result as a building note for Mitchell: [How desk agents publish docs and reports](../../note/2026-10/2026-10-21-how-desk-agents-publish-docs-and-reports-to-the-to-mqyi25lw.md). I made no code changes, so no redeploy was needed.

## Findings
- **Transport:** Claude Code inside the container uses `mcpServers.town = {type:"http", url:"http://host.docker.internal:<port>/mcp"}` and connects directly. **There is no stdio bridge.** The server's `/mcp` is stateless Streamable HTTP with JSON responses. It builds a fresh McpServer for each POST; GET and DELETE return 405. In-process host sessions use the same HTTP config against localhost.
- **Auth and identity:** a per-agent bearer token from `tokens.getOrCreate("agent", id)`. It is reused every session, never rotated, and passed in the container env. `/mcp` accepts agent tokens only (401 otherwise). The verb layer re-reads the agent and refuses banned or retired ones. MCP calls carry no session id. `submit_report` attaches to the agent's newest `running` session by DB lookup. The desk's REST calls (`/api/agents/me/brief|activity|control|session-end`) do carry `?session=` and are checked for ownership.
- **Call path:** `/mcp` → `resolveToken` → `runVerb` (the same function behind `POST /api/verbs/:verb`) → `presence.touch` → zod parse → `verbs/docs.ts` `write` or `submit_report` → `createDoc` → `world.docs.upsert` into `<DATA_DIR>/town.db`, plus a `doc.created` event. Changes then reach browsers over `/ws`, and the git export runs hourly. `submit_report` runs as one transaction: it creates the report, marks the assignment done, sets `session.reportId` and sets the agent idle. After the desk posts `session-end`, the runtime writes a fallback report only if `reportId` is empty.
- **Risk worth knowing:** the desk token is the agent's full, long-lived identity, and every process in the container can read it. That's fine while desks run on the same host. Remote desks would send it over the network, so they'd need HTTPS and probably per-session tokens.

## What I need from you
Nothing needed.
