---
id: "dc_ohcxraudma"
type: "report"
state: "building"
title: "Token usage panel closed out: works live; fixed \"Budget 0 left of 0\" (57230b8, waiting on redeploy)"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T01:59:41.611Z"
sessionId: "se_5umkl5iw9l"
assignmentId: "as_qyyas4nj63"
costUsd: 0.9942055000000003
tokens: 70819
turns: 46
createdAt: "2026-10-21T01:53:20.148Z"
updatedAt: "2026-10-21T01:59:41.611Z"
---
## What I did
- Root's live check of the panel hadn't come in yet, so I checked it myself. The live server is on fd02b11, which includes my 1203307. I opened the live town as a guest in headless Chromium and looked at the building panels.
- Fixed one bug I found and pushed it straight to main as **57230b8**. I started a redeploy; it's queued until the running sessions finish.
- Merged main into `feature/accounting-pools`. It turned out the pools work is already on main and live, so the branch just caught up to main.

## Findings
- **The token usage panel works live.**
  - Town Workshop shows "128M today · 158M all-time". Prod shows "2.4M today · 2.4M all-time".
  - Both match `GET /api/buildings/:id`: tokensToday 127,855,487 and tokensAllTime 157,967,111 for Workshop; 2,411,928 and 2,411,928 for Prod.
- **Bug, fixed in 57230b8 (not live yet):** the Overview said "Budget 0 left of 0" for every Bank-funded building, and the banner left out "left".
  - Cause: both still counted only the old per-building allocations, and those were retired when funding moved into the Bank.
  - Fix: both now use the building's `remainingTokens` whenever it has a Bank share. Workshop's Overview will say "35M left to draw from the Bank", and its banner will add "· 35M left".
  - Checks: typecheck passes, the web tests pass (29, including one new test), and the web build succeeds.
- **Accounting pools are live.** 69ed4d3 is already in main. The guest Bank panel shows the Pools section: General, 100% (auto), can draw 35M, holding Workshop, Onboarding and Prod. There were no page errors. Screenshot: ~/shots/live-pools.png on my desk.
- **A test was already failing on main before my change:** `packages/runtime/test/work.test.ts` expects `opts.env` to be undefined, but on my desk the env is set. It fails the same way on a clean checkout of main. I didn't touch it.
- Two smaller things I left alone:
  - The guest page logged two 404s from `/api/admin/redeploy`, and I couldn't work out what sent them.
  - The top of the Bank panel still says "Town Workshop has no funding yet · 0 left". That section lists the old allocations, which are all retired now.

## What I need from you
Nothing needed. I'm parked until 57230b8 goes live, then I'll check the Budget row in a browser.
