---
id: "dc_fnlpbktrr5"
type: "report"
state: "building"
title: "Each agent runs its own Claude Code process (~0.1–0.16 GB). That's a real cost per session, but not a problem at our scale, with or without Docker"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "ok so explain to me how a claude code session can have an agent team with 10 different members, with clean contexts, running on different tasks without breaking a sweat? or does memory usage within that session actually scale up with the size of the agent team? and then there are subagents too, right? which are like agent teams but more ephemeral?"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:39:10.305Z"
sessionId: "se_u16whkv8k5"
assignmentId: "as_ufznoq15go"
costUsd: 0.3310416
tokens: 323583
turns: 11
createdAt: "2026-10-21T04:36:18.181Z"
updatedAt: "2026-10-21T04:39:10.305Z"
---
## What I did
- Read the Agent SDK we ship (`@anthropic-ai/claude-agent-sdk` 0.3.306) and how our desk runner calls it (`packages/desk/src/run.ts:219`).
- Measured a freshly started Claude Code process next to my own live session, using the unfreeable memory count (`smaps_rollup` Anonymous).
- No code changes.

## Findings
**What "the SDK" actually is.** The Agent SDK doesn't call the API itself. Each `query()` starts a separate Claude Code program and talks to it over stdin/stdout. That program is a 290 MB single file: the Bun JavaScript runtime with Claude Code's whole app bundled inside.

**Why it's heavy:**
- **Just starting it costs 94 MB.** That's what a fresh Claude Code process uses before it does any work: the JS engine plus the parsed app.
- **My live session after ~10 turns uses 158 MB.** The extra is the conversation history, tool definitions, the MCP client for the town, file caches and garbage-collector headroom.
- **The rest of the app accounts for the base cost.** API calls are only part of it. Claude Code also contains the tool implementations (Bash, Read/Edit, Grep, web fetch), permission checks, context compaction when a conversation gets long, subagents, skills and MCP.

**Can several sessions share one instance? No, not with this SDK.**
- Each `query()` gets its own process with its own working folder, environment, permissions and MCP config.
- In our setup that MCP config carries the agent's own town token, so separate processes are also what keeps agents apart.

**Without Docker: yes, the cost stays.** Docker adds almost nothing: a container is a cgroup, not a VM, and an idle desk uses 0.1 MB. Without containers we'd still pay ~0.1–0.16 GB per running Claude Code. The bigger peak is `tsc` (~0.5 GB for a few seconds), and we'd pay that either way.

**Only running sessions cost RAM.** Idle agents cost almost nothing, so the cost grows with how many sessions run at once, not with how many agents exist. At ~0.2 GB each (Claude Code plus our 50 MB runner):
- 10 sessions at once ≈ 2 GB.
- 20 sessions at once ≈ 4 GB.

**The only way to make sessions much lighter** is to write our own agent loop on the plain Anthropic API (`@anthropic-ai/sdk`) inside one Node server. That would cost a few MB per session. But we'd have to rebuild Claude Code's tools, permissions and compaction ourselves, and agents would still need sandboxes for running commands, so `tsc` would still peak at ~0.5 GB. My view: weeks of work to save about 1 GB, which costs a few dollars a month. Not worth it now.

**Bottom line:** the 8 GB VPS-2 ($8.50/mo) still runs about 20 sessions at once.

## What I need from you
Order the OVH US VPS-2 (8 GB, Ubuntu 24.04, Oregon) with an SSH key we can use, and create a Cloudflare R2 bucket.

## Reply from Mitchell (2026-10-21 00:39)

ok so explain to me how a claude code session can have an agent team with 10 different members, with clean contexts, running on different tasks without breaking a sweat? or does memory usage within that session actually scale up with the size of the agent team? and then there are subagents too, right? which are like agent teams but more ephemeral?

