---
id: "dc_081ccz6l9n"
type: "report"
state: "building"
title: "Agent teams step 1: a manager's tell now reaches a live fork mid-session (PR #138, main 6161c53)"
authorId: "ag_twyze6aigx"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 1 done: PR #138 = 6161c53, a tell from any Workshop agent reaches a live fork as an interrupt (now: true). Live check queued separately; step 4 (as_7cr9qca4of) unblocks on its own."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T01:41:21.410Z"
sessionId: "se_857oq91qhz"
assignmentId: "as_z3t85q3e0e"
costUsd: 1.3761514999999997
tokens: 68808
turns: 39
createdAt: "2026-10-31T01:41:11.040Z"
updatedAt: "2026-10-31T01:41:21.410Z"
---
Mitchell can now have Pix (or any agent of the Workshop) message a running fork, and the fork sees it right away, mid-task, the same way his own message to a fork does.

## What I did
Built step 1 of [dc_i7ji4xacd9](../../article/2026-10/2026-10-31-forks-vs-claude-code-agent-teams-the-gaps-ji4xacd9.md). PR https://github.com/mitchellgordon95/muster-town/pull/138: CI is green and it is merged as **6161c53**. I queued a redeploy, so 6161c53 should be live. I have not checked that yet.

## Findings
- **Rule chosen: any agent whose home building is the fork's building.** That covers the manager, sibling forks and residents. It is simpler than "manager only" and matches agent teams, where any teammate can message any other. Agents from other buildings still reach only the inbox.
- **What changed in the code:**
  - `tell` in core/src/verbs/social.ts: when the recipient is a live fork (has `forkOf`, is not retired, and `isWorking` is true) and the sender is from its building, it also calls `interruptNow` from core/src/wakes.ts. I exported that function along with `isWorking`.
  - `interruptNow` is the path the human-message and wake interrupts already use. A session running inside the server process gets it through `host.interrupt`. A desk session gets it through the interrupt queue (GET /api/agents/me/control).
  - It uses `now: true`, the same as a human's message. Without it, a desk session, which is one long turn, would only see the message at the end.
  - The message still lands in the fork's inbox, and `tell` returns the note "delivered as an interrupt".
- **Prompt and manual:** the manager prompt (`teamBlock`, core/src/memory.ts) no longer says "forks don't take messages". It now says a `tell` to a live fork reaches it mid-session as an interrupt, and that mail sent after the fork's session ends goes to the manager. I also updated one line in docs/manual.md. My first wording went over the manual's 1,900-word cap and failed CI once; I shortened it.
- **Test:** new runtime test in runtime/test/forks.test.ts. A tell from an agent in another building leaves the fork's inbox message and adds no interrupt. Mei's tell lands in the inbox, adds exactly one interrupt with `now: true`, and the fork receives "Mei told you … Also cover C" as its next streamed message. Locally core 513/513, runtime 175/175 and typecheck all pass.
- **Next session's live check:**
  1. GET /api/health shows a commit containing 6161c53.
  2. Pix tells a running fork.
  3. GET /api/events shows "Interrupt for Pix N: Pix told you…", and the fork answers without calling `inbox`.
- Topic page with the state and steps 2-4: [dc_qhgxudus5c](../../wiki/2026-10/2026-10-31-agent-teams-forks-vs-claude-code-agent-teams-gxudus5c.md).

## What I need from you
Nothing needed.
