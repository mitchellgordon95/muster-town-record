---
id: "dc_8npkzuqxoo"
type: "report"
state: "building"
title: "Hosted collectives step 5 is on main as 85ab93b: each hosted collective runs its own agents on the owner's API key, held with \"No key yet\" until a key is added"
authorId: "ag_kc552jb67x"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 5 accepted as built (85ab93b: in-process host runtime per hosted collective, scrubbed env, keyHold, 1 running, no redeployer). I queue the redeploy now; the live check goes to you as a separate assignment gated on the deploy."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T23:29:49.280Z"
sessionId: "se_0jsd0aw5wd"
assignmentId: "as_cfnk09jn84"
costUsd: 2.7377458000000012
tokens: 136887
turns: 64
createdAt: "2026-10-27T23:24:29.863Z"
updatedAt: "2026-10-27T23:29:49.280Z"
---
## What I did
I built step 5 from wiki dc_ggx7ze1ahy and followed Kelly's direction (ms_arhzliuuw0): hosted collectives get in-process sessions only, one running at a time, and no Fly Machine desks. I pushed it straight to main as **85ab93b**. I couldn't queue the redeploy myself because I don't have town.redeploy, but one was already waiting on my session, so it should pick up 85ab93b.

## Findings
- **Runtime per hosted collective** (`startRuntime({ hosted: { dir } })`):
  - Started in server main.ts once the server listens. Collectives opened at boot start then; one created through POST /api/collectives starts as soon as it is mounted.
  - Its MCP endpoint is `/<slug>/mcp` and it exports to `<dir>/export`.
  - When a collective is retired, its runtime stops before its World closes.
- **Scrubbed env** (`hostedEnv`, runtime/src/sdk.ts):
  - It is built from scratch with no host `CLAUDE_*`, `ANTHROPIC_*` or `XDG_*`. HOME is `<dir>/home` and CLAUDE_CONFIG_DIR is `<dir>/claude`.
  - fundingFor, sessionEnv, oneShot and deskAuth all read it, so the Workshop's key, its subscription token and `~/.claude` never reach a hosted session.
- **No-key hold** (core `budget.keyHold`):
  - A hosted World with no live API-key input of its own holds all work. The assignment's heldReason is "No key yet: add your Anthropic API key at the Bank".
  - Agents stay idle, not out of budget, and work starts on the next tick after an admin adds a key.
  - As a backstop, a hosted session whose funding has no key is refused before the SDK is called. This covers work, manage, chat, Ask about and summaries.
- **Desks and host actions:**
  - Hosted collectives use the host backend only: town tools and web, no shell, no file tools. Code buildings are not scheduled.
  - `HOSTED_MAX_RUNNING = 1` per collective.
  - There is no redeployer: a hosted admin's redeploy gets 403, and the GitHub and Fly tokens are never read.
  - All of this is written into docs/hosted-collectives.md item 5.
- **Adding the first resident:** a new collective starts with `buildings: []`. The stranger opens Planning → New building (Desks = how many residents), adds the key at the Bank, then gives a resident an assignment. The manual already covers the key part.
- **Workshop unchanged:** its runtime gets no `hosted` option, so funding, env, desks and redeploy go through the same code paths as before. A test checks that the Workshop still sees the host env and still has redeploy.
- **Tests:**
  - New file runtime/test/hosted.test.ts, 4 tests: no key means held with nothing sent to the SDK; with the owner's key the session runs on it, and no host key, token or `/root/.claude` appears in the options; slots max is 1 and redeploy is refused; the Workshop is unchanged.
  - Full suites, run to completion: core 357/357, runtime 135/135, server 111/111. Typecheck is clean.
  - Those full suites ran before I rebased onto main. Main had picked up forks step 2 (dde6f86), which conflicted in one import line. After the rebase I re-ran typecheck (core, runtime) and the hosted, forks and work tests: 19/19 pass. I did not re-run the full suites after the rebase.
- **Not live-checked.** Once 85ab93b is live, a human can check:
  1. Start a collective without a key, create a building, and assign work: it stays held with "No key yet".
  2. Add a key at the Bank: a session starts within about 5 s and shows "funded by API key".

## What I need from you
Nothing needed, as long as the waiting redeploy goes ahead. If it doesn't, someone with town.redeploy needs to queue one so 85ab93b goes live.
