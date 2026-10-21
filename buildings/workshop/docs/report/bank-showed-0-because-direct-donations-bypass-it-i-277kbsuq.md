---
id: "dc_j9277kbsuq"
type: "report"
state: "building"
title: "Bank showed 0 because direct donations bypass it; it now counts tokens held by buildings (5a9f291 on main, redeploy started)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "i think we change my donation data to be to the bank, not the building. but you can keep that \"owned by buildings\" stat, it should just be 0 for now"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T20:47:00.840Z"
sessionId: "se_nv8vuo4zwq"
assignmentId: "as_48vmy97ajf"
costUsd: 0.7934969000000001
tokens: 999562
turns: 21
createdAt: "2026-10-20T20:44:06.223Z"
updatedAt: "2026-10-20T20:47:00.840Z"
---
## What I did
Read the live `/api/bank` and `/api/budget` and the Bank and budget code. Changed the Bank summary and its UI so they count tokens donated straight to buildings, added a core test, then pushed to main as **5a9f291** and started a redeploy. It also carries Lena's minimap and Sage's town planning.

## Findings
- **Cause:** it wasn't a reset from the redeploy, and it wasn't a display glitch. The Bank's balance only counts Bank inputs: API keys and the owner's subscription. The live town has **0 inputs**, so the balance really was 0.
- Mitchell's **350,000,000 tokens** were donated directly to the Town Workshop. Those are allocations held by the building, which the Bank never counted. **133,907,553** are spent and **216,094,416** are unspent. The Onboarding building holds **0**.
- So a direct donation does credit the building, just not the Bank. The Bank sign said "tokens available to the town" while leaving out every token held by a building.
- **Fix:** `BankSummary` now has `heldTokens` (total and per building) and `townTokens` (= Bank balance + held).
  - The sign's headline is the town total, with a third column, HELD BY BUILDINGS.
  - The Bank panel lists the town total, what's in the Bank, and what buildings hold.
  - The Shares table has a Held column, and the Bank map's title shows the held amount too.
  - After the redeploy the sign should read about 216M.
- **Verified:** a new core test covers the live case (no inputs, only direct donations). Typecheck and all suites pass (171 core tests and others). I didn't look at the new sign in a browser.
- **Funding Onboarding works today:** at the Bank, choose Donate → "Give to: One building" → Onboarding. Giving to "The Bank" needs either an API key or the owner's subscription input, and then the Bank splits it 50/50 between the two labs. There's still no way to move the Workshop's unspent tokens to another building, even though the `town.allocate_budget` permission is described as doing that. I didn't build it.

## What I need from you
Nothing needed.

## Reply from Mitchell (2026-10-20 16:47)

i think we change my donation data to be to the bank, not the building. but you can keep that "owned by buildings" stat, it should just be 0 for now

