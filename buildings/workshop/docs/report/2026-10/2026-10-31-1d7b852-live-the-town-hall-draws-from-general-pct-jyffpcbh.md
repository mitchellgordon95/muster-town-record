---
id: "dc_8gjyffpcbh"
type: "report"
state: "building"
title: "1d7b852 live: the Town Hall draws from General (pct 100); Planner can start as far as the API shows"
authorId: "ag_3rbk94vhuw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ujc1l2z1mh","mt_cz11aqe81a"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/137"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: 1d7b852 live (health 6161c53), Town Hall in General at pct 100, Town Hall budget = Bank balance; crop mf_qodw723g9z for rollup 34. Planner end-to-end stays Mitchell's \"Your call\" (needs a signed-in human)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T01:52:36.495Z"
sessionId: "se_is626um9tu"
assignmentId: "as_g5h18xqiym"
costUsd: 0.8641536999999997
tokens: 43208
turns: 25
createdAt: "2026-10-31T01:52:18.882Z"
updatedAt: "2026-10-31T01:52:36.495Z"
---
## What I did
Checked the live town at about 01:50Z against PR #137 (merge 1d7b852), using guest and API access. Took one crop and rewrote the topic pages [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md) and [dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md). I changed no code.

## Findings
- **The fix is live.** GET /api/health shows commit 6161c53, and `git merge-base --is-ancestor 1d7b852 6161c53` succeeds, so 1d7b852 is in it.
- **GET /api/bank:** the Town Hall is listed in the General pool with `pct` 100 (auto), the same as every other building. General's `buildings` list includes the Town Hall. Bank balance is 20,140,737 adj. tokens. The daily cap is not held (`held: false`, about 2.75M spent today).
- **GET /api/buildings/town-hall:** `budget.remainingTokens` is 20,140,737, the same as the Bank balance. So `Budget.canStart` has funds for a Town Hall agent, and `PLANNER_UNPAID` should not post now.
- **Not tested end to end: the Planner itself.** The Planner agent doesn't exist yet; it is created on the first "Plan with an agent". POST /api/planner/one-on-one returns 401 for a guest. A real Planner 1:1 still needs a signed-in human, which is the "Your call" line for rollup 34.
- **Visible change:** Bank → Pools now lists the Town Hall among General's buildings. Crop ![pools](/api/media/mf_qodw723g9z.png) (mf_qodw723g9z, 490×176).
- Step 7 (as_3xd2xv78h1) no longer waits on this.

## What I need from you
Nothing needed.
