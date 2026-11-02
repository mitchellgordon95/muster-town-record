---
id: "dc_t0c4khsl0r"
type: "report"
state: "building"
title: "Reports: \"Ask about this\" replaced by \"Talk to <author>\" (1:1 with the author); 2b28c0a on main, live check parked"
authorId: "ag_0c4tzo8gtp"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. \"Talk to <author>\" is on main at 2b28c0a; the live check and screenshot are already queued as as_yj8o64f1hj (waits for deploy 2b28c0a, CI redeploys). The fork's missing town.redeploy permission is covered by as_t3ap7woooy, already pending. Goes into rollup 30 as a Shipped item once the live check passes."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T22:17:38.858Z"
sessionId: "se_lkfapcf8xj"
assignmentId: "as_oz9ose9lzo"
costUsd: 2.7615372999999988
tokens: 138077
turns: 56
createdAt: "2026-10-28T22:17:29.419Z"
updatedAt: "2026-10-28T22:17:38.858Z"
---
## What I did
I removed "Ask about this" and added a **Talk to <author>** button to every report. The button opens a 1:1 that reuses the existing one-on-one path, extended so it takes an agent and a report. I committed 2b28c0a straight to main. The `redeploy` tool refused: I don't have the town.redeploy permission. CI redeploys main once it's green, so this session is parked until 2b28c0a is live. The live check and the screenshot happen then.

## Findings
- **Removed:**
  - the in-tray AskBox and its CSS
  - `api.ask`
  - POST /api/docs/:id/ask (it now returns 404)
  - runtime `askAbout`
  - schema `AskInput`
  - the two tests that only served it

  The feature stored nothing, so no table needs keeping.
- **What a human sees:** reports open through DocView in the in-tray, filing cabinet, board and library. Every report there shows a primary **Talk to Lena** button (the author's name) to a signed-in human who can facilitate or review in the target agent's building. Clicking it opens the meeting panel on the 1:1.
  - For a fork's report the button reads **Talk to Pix**, with "Pix 1 is a fork of Pix, so Pix answers".
  - For a report by a retired or stopped resident, it names the building's manager and says why.
- **Core:** `createOneOnOne(world, human, buildingId, { agentId, docId })` makes that agent the facilitator.
  - The human's first line presents the report as a doc attachment, with its id in the text. The 1:1 prompt therefore carries the id and tells the agent to `read` it.
  - If the human already has an open 1:1 with that agent, the same meeting is returned. A report not yet shown in it is presented once.
  - With no body, the route still opens the manager's 1:1 as before.
- **Runtime:** before this change only managers could answer a 1:1. `wakeManager` now also wakes any resident that a human opened a 1:1 with. The resident answers in its own host session ("manage" purpose, no in-tray), which ends when the 1:1 ends. A resident that is busy in a work session answers once that session ends.
- **Tests (all pass on the desk):**
  - core `one-on-one.test.ts` covers the new path, plus the fork and gone-author targets.
  - server `rest.test.ts` covers the route with agentId and docId, and that /ask returns 404.
  - runtime `one-on-one.test.ts` checks that a resident answers its 1:1 and that the prompt contains the report id.
  - web `talkToAuthor.test.tsx` checks that DocView renders "Talk to Lena" and not "Ask about this".
  - Also run: manage, waker, redeploy, meetings-chat-scheduler and manual tests; `tsc` per package; check:docs.
  - The runtime 1:1 tests need `--testTimeout=60000` on a desk; at 5 s they time out only because the desk is slow.
- **Small side change:** `useTown` now passes a server snapshot, which lets `renderToStaticMarkup` tests render store-backed panels.
- **Manual:** the "Ask about this" sentence in docs/manual.md is replaced. The word-cap test passes.
- **Topic page:** [dc_vrrph0d7ss](../../wiki/2026-10/2026-10-28-talk-to-the-author-1-1-docs-and-grants-rph0d7ss.md) records this state for the next session.

## What I need from you
Nothing needed: once CI redeploys 2b28c0a, the parked session resumes and does the live check and screenshot.
