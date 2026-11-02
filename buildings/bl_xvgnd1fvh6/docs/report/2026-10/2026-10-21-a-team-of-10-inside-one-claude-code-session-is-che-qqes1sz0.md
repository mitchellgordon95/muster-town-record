---
id: "dc_gbqqes1sz0"
type: "report"
state: "building"
title: "A team of 10 inside one Claude Code session is cheap because the thinking happens at Anthropic. Locally, each member is just a conversation history in the same process, a few MB each"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_fnlpbktrr5"],"urls":["https://code.claude.com/docs/en/agent-teams"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "so this is exactly what i'm saying. ditch multiple containers? just run everything in one process, with standing rules about how to share the filesystem. couldn't we make that work?"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:47:09.012Z"
sessionId: "se_b2u1vucmxg"
assignmentId: "as_t0edzhe75b"
costUsd: 0.60578492
tokens: 27690
turns: 22
createdAt: "2026-10-21T04:42:47.967Z"
updatedAt: "2026-10-21T04:47:09.012Z"
---
## What I did
- Launched 5 subagents from my own session at the same time and sampled my Claude Code process every second (process count, unfreeable "Anonymous" memory, threads).
- Read the official agent-teams docs and checked the teammate modes compiled into our Claude Code binary.
- No code changes.

## Findings
**Why it doesn't "break a sweat":** the model doesn't run on our machine. A session, subagent or teammate is mostly a conversation history: a list of messages kept in memory and sent to the API on each turn. A "clean context" just means a new, empty list. Ten members means ten lists plus ten HTTP requests in flight, and the process mostly sits waiting on the network. Most of a session's memory is the ~94 MB fixed cost of the program itself (JS runtime plus app code), and every member running inside it shares that.

**Subagents (measured):** they run inside the parent process, not as new ones.
- 5 subagents running at once: still **1 Claude Code process** the whole time.
- Memory went from **149 MB to a peak of 182 MB**, about **+33 MB for 5**, or **~7 MB per subagent** (they were small tasks: 1–2 file reads, ~15–22k tokens each). It settled back to ~170 MB once they finished.
- Inference: memory does grow with team size, but slowly and roughly in step with how much text each member holds. A subagent with a big context (say 150k tokens, about 0.6 MB of text plus tool output and overhead) might cost tens of MB. That part is my estimate; I didn't measure it.
- You're right that they're ephemeral: a subagent gets its own context, does one job, hands back a result and ends.

**Agent teams:** these are the longer-lived version. Teammates message each other directly and share a task list. Memory depends on the display mode (from the docs and the binary's settings: `in-process`, `tmux`, `iterm2`, `auto`):
- **In-process (the default):** every teammate lives in the lead's process, so it costs about what a subagent does.
- **Split panes (tmux or iTerm2):** each teammate is a separate Claude Code process, so each one costs about the same ~0.1–0.16 GB as one of our desks.
- Teams are experimental, need `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`, and per the docs they don't spawn in non-interactive/Agent SDK sessions. Our desks therefore get subagents only.

**What this means for us:** a town agent is a separate process (~0.2 GB with our runner) because it needs its own identity (its own town token), folder and sandbox. A subagent doesn't need any of that. Each extra session costs us RAM, and that is the price of keeping agents apart. Each extra subagent inside a session costs only a few MB. The tokens, which are the real cost, grow with the number of members either way. The 8 GB VPS-2 conclusion stands.

Sources: my measurements on this desk (agent-sdk 0.3.306, arm64); https://code.claude.com/docs/en/agent-teams

## What I need from you
Order the OVH US VPS-2 (8 GB, Ubuntu 24.04, Oregon) with an SSH key we can use, and create a Cloudflare R2 bucket.

## Reply from Mitchell (2026-10-21 00:47)

so this is exactly what i'm saying. ditch multiple containers? just run everything in one process, with standing rules about how to share the filesystem. couldn't we make that work?

