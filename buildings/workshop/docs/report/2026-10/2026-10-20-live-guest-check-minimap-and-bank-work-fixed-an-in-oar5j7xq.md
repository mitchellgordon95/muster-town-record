---
id: "dc_0hoar5j7xq"
type: "report"
state: "building"
title: "Live guest check: minimap and Bank work; fixed an inflated leaderboard figure"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T21:36:38.910Z"
sessionId: "se_0ff6fhnofj"
assignmentId: "as_vxiukgus87"
costUsd: 0.7502190000000002
tokens: 40254
turns: 32
createdAt: "2026-10-20T21:28:48.142Z"
updatedAt: "2026-10-20T21:36:38.910Z"
---
## What I did
I opened the live town (commit 98cdae4, which was main HEAD) in headless Chromium as a guest (`/?guest`). I tested the minimap and the Bank panel and took screenshots. Then I fixed one Bank bug I found, committed it to main as 68961fb, and queued a redeploy.

## Findings
- **Minimap works.** It sits in the bottom-left (232×164 px) and draws the buildings with their labels and the viewport box. Clicking it walks the guest's body there, and the scroll wheel zooms it. It hides in the Bank town-map overview, as designed. There were no console errors and no HTTP errors (≥400).
  - One cosmetic issue: the "Town Workshop" and "Town Hall" labels overlap on the minimap.
- **Bank as a guest works.**
  - The sign shows 69,695,982 tokens: 19,695,982 expire today, 50,000,000 are permanent, 0 are held by buildings.
  - The panel shows the inputs (20M/day subscription, 50M one-time API key) and the shares (Workshop 80%, 56M; Onboarding 20%, 14M).
  - Donating and funding a building correctly show "Sign in with GitHub" to a guest.
  - The town map's flow arcs and labels match these numbers.
- **Bug, now fixed:** the Top contributors list showed **Mitchell at 1070M** while the Bank holds 70M.
  - Cause: the list added in the 1000M of direct allocations that were retired when funding moved into the Bank. Only about 138.9M of that was ever spent (600M sub: 1.7M spent; 300M: 87.2M; 50M: 50.0M; 50M buffer: 0).
  - Fix (`packages/core/src/bank.ts`): direct donations are now added up from the allocations themselves. A retired allocation counts only what was spent from it.
  - Once 68961fb is live, Mitchell should show about 209M (70M from the Bank plus 138.9M spent).
  - I added a unit test. Typecheck passes, and the core (178) and server (56) tests pass.
  - I have not seen the fix live yet: the redeploy is queued until the running sessions finish.
- `/api/budget` `users.donated` still reports the raw 1000M. I left it alone because nothing guest-facing shows it.

## What I need from you
Nothing needed.
