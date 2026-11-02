---
id: "dc_btyi8imkjg"
type: "report"
state: "building"
title: "Goal tree cards now say \"moves under\"; retiring a goal with a building attached asks to confirm, naming each building (PR #154, 2cc2796, redeploy queued)"
authorId: "ag_wjyl2liqlm"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_n25udpflus","dc_hsq0e5a587"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/154"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #154 merged 2cc2796; included in e97dd9c (PR #155 merged main). Live check covered by the e97dd9c check. Rollup 34 Shipped item with crop mf_9gve8qmz1g."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T05:01:27.255Z"
sessionId: "se_2id6n6i477"
assignmentId: "as_qjvuoscwq8"
costUsd: 1.5511248999999996
tokens: 77556
turns: 37
createdAt: "2026-10-31T04:46:42.193Z"
updatedAt: "2026-10-31T05:01:27.255Z"
---
## What I did
A move card now reads **"Make Muster Town beautiful and intuitive moves under Steer (goal-directed)…"**, with no bare "→". A retire card reads **"Ship improvements… is retired; its open key results and attached buildings go under Steer…"**. If nothing open hangs under the goal, it reads "…is retired; nothing open hangs under it".

When a building is attached anywhere under the goal, Mitchell no longer gets a one-click retire. On a retire proposal, Accept becomes **Accept…**, and in the Retire form the button becomes **Retire goal…**. Either one opens a confirmation that names each building and open key result that moves (for example "Town Workshop moves under Steer (goal-directed)…") and says "A building is never archived here; it moves". It has **Accept and retire** / **Cancel** buttons.

The review deck uses the same card, so a deck Accept asks for the same confirmation. The deck slide's text also uses the same words and lists "What moves under …".

PR https://github.com/mitchellgordon95/muster-town/pull/154, merged as **2cc2796**. Redeploy queued; 2cc2796 should be live next. I have not checked it live.

## Findings
- Before/after crop, 300 px tall: mf_9gve8qmz1g. It is a static render of the real components with styles.css. It shows the Accept… button and the confirmation open together; in the app the confirmation appears only after clicking Accept….
- Code:
  - Web: `proposalVerb` and `retireMoves` in `panels/goalTree.ts`, and `RetireConfirm` in `GoalTreePanel.tsx`, used by both ProposalCard and RetireForm.
  - Core: `goalProposalVerb` in `review-deck.ts` uses the same words. A new `Goals.retireImpact(id)` is now used by both `retire` and the deck slide.
  - No migration.
- Edge case: a retire proposal with no sibling named but something still under the goal now says "is retired, but no sibling is named for what hangs under it", instead of wrongly saying "nothing open hangs under it". The server refuses to accept that proposal, as before.
- Tests:
  - Core `goals-step4.test.ts`: the deck's move and retire words, plus the "What moves" line naming the building and the key result.
  - Web `goalTree.test.tsx` (renamed from .ts so it can hold JSX): the verbs, the card markup, Accept… shown only when a building is attached, and the confirmation's text and buttons.
  - `npm run check --fast` passed (4m53s). The branch had no CI checks.
- Not checked: clicking through the confirmation needs a signed-in human, so only the static render and the tests cover it. Topic page [dc_hsq0e5a587](../../wiki/2026-10/2026-10-31-goal-tree-editor-ux-flag-dc-yn8gl1rmyt-q0e5a587.md) is rewritten with these changes.

## What I need from you
Nothing needed.
