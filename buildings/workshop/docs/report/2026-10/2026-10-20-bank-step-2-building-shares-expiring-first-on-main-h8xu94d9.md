---
id: "dc_60h8xu94d9"
type: "report"
state: "building"
title: "Bank step 2 (building % shares, expiring-first) on main as 58ffd25; #30/#32 closed; needs one more redeploy"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T18:46:11.405Z"
sessionId: "se_zjot0yv8cv"
assignmentId: "as_x4g2tk5hy7"
costUsd: 2.065431
tokens: 3553607
turns: 51
createdAt: "2026-10-20T18:39:13.817Z"
updatedAt: "2026-10-20T18:46:11.405Z"
---
## What I did
- Checked the live server. `GET /api/bank` returns HTTP 200: `{"balanceTokens":0,"creditedTokens":0,"dailyInflowTokens":0,"inputs":[]}`. Step 1 is live, and the Bank is empty because nobody has added an input yet.
- Built Bank step 2 using the defaults Pix's follow-up assignment set (as_dlhaaa9hku). Pushed it straight to main as **58ffd25**.
- Closed PRs #30 and #32 as superseded, with a comment on each.

## Findings
**What step 2 does**
- **Shares.** Each building gets a percentage of the Bank. An admin can set a building's share with `PUT /api/bank/shares/:buildingId {pct|null}`. Explicit shares can't add up to more than 100%. Labs without a set share split the rest equally. Town Hall gets 0% unless it's given a share. Shares apply to what the Bank holds now, so a change takes effect right away.
- **Expiring vs durable.**
  - Subscription credits expire at the next daily renewal, so unused quota doesn't roll over.
  - API-key credits are durable: they stay until spent.
  - A building's share is spent in this order: subscription credits first (soonest to expire first), then API-key credits, then the building's existing allocations.
  - Every draw is recorded as a row in a new `bank_debits` table (migration 017).
- **No hard stop.** A session always finishes and is charged afterwards. If it spends past what's left, the extra goes onto an allocation if the building has one. Otherwise the building's API-key share goes negative and is paid back from later credits. Agent caps are unchanged.
- **Budget and runtime.**
  - A building's `remainingTokens` now includes its Bank share (shown separately as `bankTokens`). That means `canStart` counts the Bank too.
  - Sessions funded from the subscription share run on the server's own login.
  - Sessions funded from the API-key share run on the key of the oldest active API-key input.
- **API.** `GET /api/bank` now also returns `expiringTokens`, `durableTokens`, and a `buildings[]` list with each building's share and what it can still draw.
- **No change on the live town until someone adds an input.** The Bank is at 0, so every building keeps running on its allocations exactly as before.

**Your open questions, with the defaults I built in**
1. **#30 (30M per-agent cap):** this was never on main; the default is still 10M. Following the decision that agent caps stay as they are, I closed #30 without applying it.
2. **#32 (building daily pool):** closed. Building shares of the Bank replace it.
3. **Expire vs roll over:** subscription tokens expire every day; API-key tokens never expire.
4. **Hard stop:** none. Sessions can overshoot, and the overshoot becomes a debt on the building's share.
5. **Shares:** labs split equally by default, and you can override any building.

All of these are easy to change if you want something different.

**How I verified it**
- `npm run typecheck` is clean and all tests pass (core 144, server, runtime and the rest).
- Three new tests in `packages/core/test/bank.test.ts`:
  - the equal split, admin-only shares, and the 100% limit;
  - spending order, overshoot debt, and that subscription credits don't roll over;
  - charging draws from the Bank before allocations.
- I extended the bank block in the REST test and updated the v1.1 migration test.
- `docs/architecture.md`, `README.md` and `docs/log.md` are updated.

**Not live yet.** Sage's redeploy pulled main just before my push. It is now draining and waits for my session and Sage's to end, so it will restart without 58ffd25. Calling redeploy again only returned `{"running":true}`.

**Next:** step 3 is the Town Hall view of the Bank. Pix's pending assignment as_dlhaaa9hku is fully covered by this session and can be cancelled.

## What I need from you
Run one more redeploy after the current one restarts, so 58ffd25 goes live.
