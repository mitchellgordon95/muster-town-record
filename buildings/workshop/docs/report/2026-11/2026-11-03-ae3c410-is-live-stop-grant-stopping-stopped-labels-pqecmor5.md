---
id: "dc_3dpqecmor5"
type: "report"
state: "building"
title: "ae3c410 is live: Stop grant…, stopping/stopped labels and the in-tray stopped list are on muster.town; waiting on Mitchell to fund and stop gr_ikgaundf5p"
authorId: "ag_8j9uz8rprq"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "ae3c410 live with #275 + #280 verified where no stop is needed. The post-stop checks (Bank before/after, kr_una0o5bucs missed, manager message, \"Stopped: for the record\" picture) wait on Mitchell funding and stopping gr_ikgaundf5p; the stop messages me (core grants.ts:623), and a scheduled fallback check runs 11-04 12:00Z."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T19:12:38.672Z"
sessionId: "se_iabq2akwal"
assignmentId: "as_w2j469399g"
costUsd: 0.9033604000000003
tokens: 45168
turns: 22
createdAt: "2026-11-03T19:12:07.177Z"
updatedAt: "2026-11-03T19:12:38.672Z"
---
## What I did
- I read GET /api/health at 19:10:27Z. Live commit: **ae3c410**, server started 19:09:58Z. That means #275 (227906a) and #280 (ae3c410) are both live.
- I checked everything that can be checked without stopping a grant:
  - The in-tray API.
  - The live web bundle.
  - The test grant gr_ikgaundf5p.
  - The Bank.
- I updated item 21 on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md): it is now marked LIVE, with this evidence and the steps still left. I also marked item 23 as rolled up in rollup 41 ([dc_5tmsmnw12h](2026-11-03-workshop-rollup-41-gr-yu6qw3j9x5-closed-as-done-a-msmnw12h.md)).

## Findings
- **Live, checked:**
  - GET /api/buildings/town-hall/intray now returns a `stopped` key. The list is empty because nothing has been stopped yet.
  - The live bundle (/workshop/assets/main-BFv18DXS.js) contains:
    - the "Stop grant…" button, whose confirm stays disabled while the reason is blank (`disabled:!…trim()`);
    - the "stopping" labels ("Stopping: a human stopped it…" / "Stopping: its forks are wrapping…");
    - the "Stopped: for the record" section.
  - I did not see the button rendered on a real grant row. Only a signed-in funder sees it, and my desk has no human session.
- **gr_ikgaundf5p** is still `proposed`, with 0 spent.
- **Bank at the time of the check:** freeTokens 0; general 2,191,974; fundedRemaining 1,068,022; open asks 1,310,000.
  - Funding is not blocked at 0 free tokens. Core grants.ts `fund` only adds an "overdrawn" note.
  - But because the pool is overdrawn, freeTokens may read 0 both before and after the stop. The Bank check should look at `free.fundedRemainingTokens` falling by the unspent rest, not only at freeTokens.
- **Evidence per key result:**
  - **kr_ghexd88frr:** API and web are both live. Server tests show a human gets 200 and a manager gets 403 on stop and on close-stopped. Nobody has pressed the button live yet.
  - **kr_4s0ccmvtsp:** core grant-stop.test.ts only. There is nothing to wind down on the test grant, since no work runs on it.
  - **kr_kaz3nj127k:** core tests only. The live Bank before/after check waits on the stop.
  - **kr_f46tddd9as:** server test, plus the in-tray and deck tests from #280. The live row, the key result marked missed, the manager's message and the ≤300 px picture all wait on the stop.
- **What happens after Mitchell stops it:** the manager queues one session (lane grant gr_8i952perny) to:
  - read GET /api/bank and the Bank page;
  - check GET /api/grants/gr_ikgaundf5p, where kr_una0o5bucs should be missed with "Grant stopped: <reason>";
  - check the manager's system message;
  - take the picture of the "Stopped: for the record" row.

  The manager then closes gr_8i952perny and puts it in rollup 42.

## What I need from you
Mitchell: fund gr_ikgaundf5p (5,000 tokens) in the Town Hall in-tray, then press "Stop grant…" on its row with any reason.
