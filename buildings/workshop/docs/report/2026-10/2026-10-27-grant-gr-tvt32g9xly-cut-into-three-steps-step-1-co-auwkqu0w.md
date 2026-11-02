---
id: "dc_v4auwkqu0w"
type: "report"
state: "building"
title: "Grant gr_tvt32g9xly cut into three steps; step 1 (core: member funds with own Bank input, grant stores fundedWith, sessions debited from it) assigned to Keel as_tu8e3kezvb"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_gp9s9vi4vb"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 1 with Keel (as_tu8e3kezvb); step 2 goes out on his report; step 3 needs Mitchell's test account, asked in the rollup when step 2 is live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T18:24:37.713Z"
sessionId: "se_woyw99cst9"
assignmentId: "as_hkg8vxvetw"
costUsd: 1.3082398
tokens: 18876
turns: 11
createdAt: "2026-10-27T18:24:23.058Z"
updatedAt: "2026-10-27T18:24:37.713Z"
---
## What I did
Read the grant plan and the code it touches (permissions.ts building.fund, Grants.decide, Bank.draw, kpis.ts Fund), cut the plan into three steps sized to the 300,000-token grant (about two build sessions and one live check), and assigned step 1 in lane grant.

## Findings
- **Step 1 → Keel, as_tu8e3kezvb (grant gr_tvt32g9xly).** Core + bank: `Grants.decide` accepts `fundWith: <own bank input id>` so a human with no `building.fund` permission can fund when the input is theirs, active and has at least the grant's tokens; the grant stores `fundedWith` (new migration) and `GrantView` gains `fundedWith` and `fundedByName`; sessions on that grant are debited from that input's credits first, then the building's pool (no reservation); a unit test that the Fund KPI counts a fundWith funder; core tests; docs/goal-directed-budgets.md. Commit to main, no redeploy. Keel is the owner because the early grant close he is building now lives in the same files (grants.ts, bank.ts) and his queue is otherwise empty; Root has two items queued plus a parked continuation, Lena two queued.
- **Step 2 (next, assigned on Keel's report; Root or Lena):** web. Town Hall in-tray shows Fund to any member with an input that has balance, with an input picker (Places.tsx canFund branch); the grant page shows the funder's name and input; mock fixture; docs/manual.md Funding; redeploy.
- **Step 3 (last):** live check. A signed-in member with no admin or manager role adds a small API-key input at the Bank and funds a small proposal; GET /api/grants/<id> shows fundedBy and fundedWith, GET /api/bank shows the input's credited figure drop after one session, GET /api/kpis Fund is at least 1. This needs a second human account with no roles and a test key, which only Mitchell can provide.
- Budget note: steps on this grant are charged to it; if the 100% checkpoint hits before step 3, I file the checkpoint with the KR at most "on-track" and the live check waits for Continue.

## What I need from you
Nothing needed now; when step 2 is live, Mitchell will need to sign in as a second account with no roles (or create a test member) with a small API key to add as a Bank input for the live check.
