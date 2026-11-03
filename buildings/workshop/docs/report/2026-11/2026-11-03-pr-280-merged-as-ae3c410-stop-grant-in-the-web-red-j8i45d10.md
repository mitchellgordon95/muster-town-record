---
id: "dc_inj8i45d10"
type: "report"
state: "building"
title: "PR #280 merged as ae3c410 (Stop grant in the web); redeploy queued, parked on the deploy for the live check"
authorId: "ag_ccl8adnz4c"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #280 merged as ae3c410, redeploy queued; the live check is already parked as as_w2j469399g on deploy ae3c410. The ask to Mitchell (fund gr_ikgaundf5p, then press Stop grant…) rides on the proposal row he already has; it goes in the next rollup's Shipped item for kr_ghexd88frr, not in Needs."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T18:11:28.641Z"
sessionId: "se_bqnkyklwhe"
assignmentId: "as_yn9zzmm864"
costUsd: 0.6763622
tokens: 33818
turns: 18
createdAt: "2026-11-03T18:11:17.702Z"
updatedAt: "2026-11-03T18:11:28.641Z"
---
## What I did
- PR #280 passed CI ("check" SUCCESS at head 323b62f). Main had moved to 66e5d33 in the meantime, so I merged main into it locally first. The merge was clean.
- I ran `npm run check` on the merged tree:
  - docs, knip and typecheck passed.
  - core passed (111 test files), and so did runtime (31).
  - web passed (282/282, run on its own).
  - server had one failure: the timing assertion in backup.test.ts ("main thread's timers keep firing", maxGap < 100 ms). It passed when I ran it alone (23/23), so it's a load flake.
- I merged #280 on GitHub, pinned to the head that passed CI. **Merge commit: ae3c410.**
- I queued a redeploy. ae3c410 should be live next. Live was 66e5d33 when I checked.
- I updated item 21 on the rollup materials page [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md).

## Findings
- **kr_ghexd88frr** (only a human can stop a funded grant):
  - The API part (#275 = 227906a) is live.
  - The web part (#280) is merged but not live yet. Server tests pass: a human gets 200; a manager trying to stop gets 403; a manager trying to close as "stopped" also gets 403.
- **kr_4s0ccmvtsp** (wind-down): the core test grant-stop.test.ts passes. It covers the fork being interrupted, queued work being cancelled, and the status going from stopping to stopped. Not checked live.
- **kr_kaz3nj127k** (unspent money returns): core tests pass. Pool-funded: free tokens rise by the unspent rest. Member-funded: the member's input stays at 460,000. The live Bank before/after check is still to do and needs a human stop.
- **kr_f46tddd9as** (key results missed, shown in the in-tray and deck): server test plus #280's in-tray and deck-slide tests. The live row and its picture are still to do.
- **Steps Mitchell takes to fund and stop the test grant:**
  1. Town Hall in-tray: fund the throwaway grant gr_ikgaundf5p (5,000 tokens).
  2. Once ae3c410 is live, press "Stop grant…" on its row and enter any reason.
  3. After that, the next session reads the Bank before and after (GET /api/bank and the Bank page). It also checks that the grant's key result shows missed with "Grant stopped: <reason>", and takes the ≤300 px picture of the "Stopped: for the record" row.
- **Next session (resumes when ae3c410 is live):** check without stopping anything:
  - the Stop grant… button on a funded row for a signed-in funder;
  - GET /api/buildings/town-hall/intray includes a `stopped` list.

## What I need from you
Mitchell: fund gr_ikgaundf5p in the Town Hall in-tray. Once the deploy is live, press "Stop grant…" on it with any reason.
