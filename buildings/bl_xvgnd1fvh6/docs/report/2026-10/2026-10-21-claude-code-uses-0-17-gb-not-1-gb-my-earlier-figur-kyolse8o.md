---
id: "dc_klkyolse8o"
type: "report"
state: "building"
title: "Claude Code uses ~0.17 GB, not 1 GB. My earlier figure counted file cache; sharing desks wouldn't save RAM, so VPS-2 (8 GB) is plenty"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "ok so what i'm hearing is that every agent that runs in these docker containers must run claude, and there are no ways to reduce the memory usage of the SDK.\n\nis it possible to run multiple sessions through the same instance of the SDK? and why is the SDK so heavy anyway? is it not just making API calls to generate tokens and then calling tools?\n\nand am i correct in thinking that even if we ditch docker containers completely, we'd still have this memory problem because every anthropic SDK instance that runs eats .2 GB?"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:35:21.884Z"
sessionId: "se_4k71u548b6"
assignmentId: "as_tj9qgwhtys"
costUsd: 0.5930084999999999
tokens: 473730
turns: 15
createdAt: "2026-10-21T04:31:15.503Z"
updatedAt: "2026-10-21T04:35:21.885Z"
---
## What I did
I re-measured my own desk during this live session. This time I used the cgroup's `anon` counter (memory that can't be freed) and per-process `smaps_rollup`, and I re-ran `npm run typecheck` while sampling. I also read how desks are started (`packages/runtime/src/desk/backend.ts`) and how workspaces are set up (`packages/desk/src/workspace.ts`) to answer the shared-desk question. No code changes, no redeploy.

## Findings
**You were right: my 1 GB number was inflated.** It came from `memory.current`, which also counts about 0.4 GB of file cache. Linux frees that cache whenever something else needs the memory. Here is the real, unfreeable memory (anon) for one running session:
- **Claude Code: 165 MB** of heap. Its 290 MB binary is file-backed and counted as cache. Containers built from the same image layer should share those pages; that's my inference, I didn't measure it across two desks.
- **Desk runner (node + tsx): 56 MB.**
- **Steady total: about 0.22 GB per running session.**
- **Peak: 716 MiB anon during `npm run typecheck`.** About 0.5 GB of that is the TypeScript compiler, not Claude Code. It lasts seconds.
- **Idle agents cost close to nothing.** A desk container between sessions runs only `sleep infinity` (0.1 MB). The `--memory 2g` flag (backend.ts:114) is a ceiling, not a reservation.

**Hacks to cut usage: no big win left.**
- Claude Code is a native binary. As far as I know it has no memory setting, and its 165 MB is already small.
- Running the desk runner from compiled JS instead of through tsx might save a few tens of MB. That's an estimate I haven't measured, and not worth doing now.
- The real peaks come from the compiler and tests. Those happen with or without shared desks.

**Sharing one desk with git worktrees: I don't recommend it.**
- **It doesn't save RAM.** Each agent still runs its own Claude Code and its own compiler, so we'd only skip a container that costs ~0 MB.
- **It would save disk:** about 0.7 GB of `node_modules` plus a repo clone per agent. On a 75–100 GB disk that doesn't matter at a few dozen agents.
- **It breaks isolation, which matters once strangers join.** Each agent's town bearer token sits in Claude Code's command line (the `--mcp-config` argument). Any process in the same container can read it with `ps`, so one agent could act as another. Each agent's home folder and `~/.claude` credentials would be shared too.

**What this means for the box:**
- 5 sessions at once is about 1.1 GB steady, plus ~0.5 GB for each one compiling at that moment.
- Add ~1 GB for the OS, Docker, Caddy and the server.
- That's about 3–4 GB at the busiest hour we've seen, so **the 8 GB OVH VPS-2 ($8.50/mo) is enough**, with room to spare. VPS-3 would only be extra headroom.

## What I need from you
Order an OVH US VPS-2 (8 GB, ~$8.50/mo) with Ubuntu 24.04 in Oregon, add an SSH key we can use, and create a Cloudflare R2 bucket.

## Reply from Mitchell (2026-10-21 00:35)

ok so what i'm hearing is that every agent that runs in these docker containers must run claude, and there are no ways to reduce the memory usage of the SDK.

is it possible to run multiple sessions through the same instance of the SDK? and why is the SDK so heavy anyway? is it not just making API calls to generate tokens and then calling tools?

and am i correct in thinking that even if we ditch docker containers completely, we'd still have this memory problem because every anthropic SDK instance that runs eats .2 GB?

