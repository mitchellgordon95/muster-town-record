---
id: "dc_ttzpizm053"
type: "report"
state: "building"
title: "Goal tree step 8, the funder filter: merged 85b106b (PR #151), waiting on the redeploy for the live check"
authorId: "ag_8tbpb4gop8"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_cz11aqe81a","dc_0xqyrevla1","dc_rke20gvrqr"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/151"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Step 8 merged as 85b106b (PR #151), redeploy queued; its live check is already parked on the queue (as_jtkc86p4u2, waits on deploy 85b106b), so nothing more to assign. Rollup 34 Shipped candidate: \"Funded by me\" + \"Your week as a funder\" slide (crop mf_n867x81rfp, mock data) once 85b106b is live and the live check passes."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T02:36:15.851Z"
sessionId: "se_w50azmt1jd"
assignmentId: "as_uciill1new"
costUsd: 4.782871899999998
tokens: 239144
turns: 90
createdAt: "2026-10-31T02:36:07.153Z"
updatedAt: "2026-10-31T02:36:15.851Z"
---
**What a funder now sees that they did not before:** a signed-in person who has put money or an API key into the Bank gets a **Funded by me** button in the Town Hall in-tray, next to Mine / All. Clicking it narrows the list to the items under the goals their money reached. In that view, "Review as deck" opens on a new first slide, **"Your week as a funder"**. It lists their Bank inputs, every session that ran on their key that week (what the work was, which building, which key result, which report, and how many tokens), and, for a subscription donor, their percentage of the pooled week and what that share bought. The goal tree's filter also gets "Funded by me", which dims the goals their money didn't reach, and a goal's Spend tab gets a "Funded by me" box. Guests see nothing new.

## What I did
- Built goal tree step 8 as docs/goals.md describes it. It only reads data: no new Bank booking logic and no migration.
- PR https://github.com/mitchellgordon95/muster-town/pull/151 is merged to main as **85b106b**, and I queued a redeploy. **85b106b should be live next.** I parked this work until that deploy, then I'll do the live check.
- Updated topic pages [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md) and [dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md), plus docs/goals.md (step 8 marked **Built**), docs/bank.md and docs/log.md.
- **This closes the 8-step goal tree build order.** The rest of step 7 is still open: removing pools, free funds, the desk's key cap, `dailyLimitTokens`, and showing a key's usage to its donor.

## Findings
- **Who paid for each session.** Each session gets one of two labels:
  - **Literal:** the session ran on a donated API key (its `credentialInputId`, whether the key is general or earmarked), or on a grant funded from a member's own input (`fundedWith`). The key's donor owns the whole session.
  - **Pooled:** every other session (it ran on a subscription, or nothing was recorded). Each subscription donor owns a pro rata share: their subscription credits in the window ÷ everyone's.
- **The code.**
  - Core `packages/core/src/funders.ts` has `funderWeek` and `funderWeights`.
  - I added four read-only Bank helpers: `inputsOf`, `inputsOfSource`, `apiKeyInputIds`, `creditsSince`.
  - The slide builder is schema `funderSlide`, so the server and the web's mock data render the same slide.
- **Routes.**
  - `GET /api/funders/:userId/week?days=7`: `me` means the signed-in human. Any other id still needs a sign-in, and a guest gets 401.
  - `GET /api/goals/:id/spend?funder=me`: literal sessions count whole, pooled sessions count at the funder's share.
- **What it will show on the live town today:** every session runs on Mitchell's Max-plan subscription, so his view is the pro rata one (100% share, no "sessions on your key" list). The literal story only appears once someone donates a key.
- **Tests:**
  - Core `funders.test.ts` (4 new tests) checks that a key donor sees the literal story with nothing booked or logged, that a subscription donor sees the pro rata story, the Spend tab filter, and the slide.
  - Also: `goals-step4.test.ts` (Spend weights), server `review-deck.test.ts` (guest 401, signed-in 200, `?funder=me`), and web `funderFilter.test.tsx` (6 tests).
  - The full `npm run check` passed. After merging main, `check --fast` passed too.
- **Crop** (mock data, since the view needs a signed-in funder): **mf_n867x81rfp**, 467×300, shows the "Your week as a funder" slide.
- **Not checked live:** the Funded by me view itself needs a signed-in human, so the live check after the deploy covers the health commit, the route's 200 and 401 answers, and the Town Hall rendering as a guest.

## What I need from you
Nothing needed.
