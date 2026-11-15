---
id: "dc_4k99v3zlbt"
type: "report"
state: "building"
title: "No raw rows for needs without an ask: PR #461 open, parked on CI"
authorId: "ag_6jxoz7lkfp"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. PR #461 is parked on CI with its continuation already queued (as_j07mah3ryb waits on pr 461: merge if green after checking migrations against main). Nothing else to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-15T22:01:49.233Z"
sessionId: "se_xkgbehh9y1"
assignmentId: "as_y7mrnayxs2"
costUsd: 3.8852008000000002
tokens: 194260
turns: 73
createdAt: "2026-11-15T22:01:36.524Z"
updatedAt: "2026-11-15T22:01:49.233Z"
---
## What I did
Checked /api/health first: commit b80f73c (PR #455) was live at 21:43Z. Read the 1:1 mt_t65exni4et transcript and decisions. Then I changed the web queue, the review deck and the ledger-rule card. Opened draft PR #461: https://github.com/mitchellgordon95/muster-town/pull/461. `npm run check --fast` passed locally (docs, knip, typecheck, tests). I also ran the affected core, server and web test files on their own. All pass.

## Findings
- **I hid them from the queue and added a plain line.** Decision 3 says "Only asks enter the queue and the review deck." So a need with no ask is never a queue item or a deck slide. That covers a proposed or held grant, an asked retainer, and a captain or join request. Hiding it completely would break the queue's rule that nothing waiting is lost. So each one also shows as one plain line with nothing to press.
  - **In the decision queue:** the line sits under the queue, e.g. "Proposal from Prod: its card is being written." A held grant reads "Held grant from Prod: …". The code is `cardsBeingWritten` in packages/web/src/panels/queueOrder.ts. It follows the same Mine / All filter as the queue.
  - **In the deck:** the state-of-the-town slide gets one line, "**Not yet on a slide:** Proposal from Prod: its card is being written." The "N decisions below" count leaves these out. When the ask is filed, the item gets its slide as before.
  - Invariant asks.md 17 now says this, with a new test in core review-deck.test.ts.
- **Ledger-rule card:** its branches are Add / Skip, not Adopt / Keep. So it now recommends Add: "Add it. The same question came back this week, and this rule answers it before it is asked again." The card also had a second gap: the policy contract needs the word "rule". So I added one sentence on what the rule does and what reversing it costs. Add still appends only the body's first line, the ledger line. policy-ledger.test.ts checks that `askStructure` comes back empty.
- **Test changes:** six core tests and four server tests read slides for grants, retainers or captain requests that had no ask. They now render the ask first, using `renderNeeds`, `seedAsk` or `verbs.ask`.
- The topic page [dc_2jqnlayllc](../../wiki/2026-11/2026-11-15-needs-and-asks-mt-t65exni4et-decision-2-qnlayllc.md) is updated.

## What I need from you
Nothing needed. The next session merges PR #461 once CI is green.
