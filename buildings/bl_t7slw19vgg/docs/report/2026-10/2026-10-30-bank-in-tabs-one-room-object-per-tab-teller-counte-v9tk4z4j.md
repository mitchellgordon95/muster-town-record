---
id: "dc_5nv9tk4z4j"
type: "report"
state: "building"
title: "Bank in tabs, one room object per tab, teller counter removed (merged f402bcf, PR #119)"
authorId: "ag_zk2z9wqy4d"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Bank tabs plan from Mitchell's 1:1 is done and merged as f402bcf. It goes into the next daily rollup."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-30T19:04:57.508Z"
sessionId: "se_ef0rgttpew"
assignmentId: "as_rybf4eodu2"
costUsd: 1.9679183000000002
tokens: 98396
turns: 48
createdAt: "2026-10-30T19:04:49.563Z"
updatedAt: "2026-10-30T19:04:57.508Z"
---
## What I did
I reused the first attempt's commit (34da702, on branch agent/teo/message-from-mitchell-…) for the room objects and sprites. I moved it onto Nell's merged Bank page (8305070) and changed it to the 5-tab plan. I opened PR https://github.com/mitchellgordon95/muster-town/pull/119, CI passed, and I merged it as **f402bcf**. A redeploy is queued, so **f402bcf should be live**. I sent the PR to Nell to check numbers and wording, and sent the commit to Cleo.

## Findings
- **Tabs** (`BANK_TABS` in schema), each opened by an object in the Bank room. The central teller counter is gone.

  | Tab | What's in it | Object | Place |
  |---|---|---|---|
  | Overview | Balance, Next 30 days, top contributors, Donate | vault | `bank` |
  | Tokens & sources | Tokens, Bank inputs, Sources | ledger desk | `bank:ledger` |
  | Pools | editable pools, Pool balances | fountain | `bank:pools` |
  | Spending | building funding, Spending, drift, out-of-tokens deaths and the cap | spending board | `bank:spending` |
  | Hosting | Fly.io | server rack | `bank:hosting` |

- **Opening a tab:** walk up and press E, or tap or click the object. This goes through the existing `PLACE_PANEL` and tap-to-interact wiring. HUD "$", `#/bank` and `#/finance` open Overview.
- **Every tab** ends with the "As of … from GET /api/…" footer.
- **Verified:**
  - `npm run typecheck` passes.
  - Tests pass: web 150/150, core 494/494, server rest + grants.
  - `finance.test.tsx` now checks that each tab has its own sections and none of the others'.
  - In the mock town in Chromium, walking to the fountain shows "E Look into the pools fountain", and E opens the Pools tab.
  - The ledger desk, spending board and town map render in the room.
- **Manual:** `docs/manual.md` was already at 1,903 words on main, over its 1,900 cap. I rewrote the Bank page line and trimmed two other lines, so it is now 1,899.
- **Not done:** the generic building-panel interior. This change is the Bank only.
- Topic page: [dc_v4itjbkgfi](../../wiki/2026-10/2026-10-30-bank-interior-tabs-and-room-objects-itjbkgfi.md).

## What I need from you
Nothing needed.
