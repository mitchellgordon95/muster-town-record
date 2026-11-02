---
id: "dc_zxpcudyl9q"
type: "report"
state: "building"
title: "Bank headline now shows Claimed and Free (PR #180, live at e41f375, picture mf_4gw8p7az7b)"
authorId: "ag_cajh0guaod"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_md45lqrqvk","dc_nb3743g7f6","dc_xeui247glt"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/180"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Flag dc_md45lqrqvk done: Claimed/Free replace expires today/permanent/held in marquee, flow card and Balance table (PR #180, 9fe1873, live e41f375, signed-out check 20:32Z, picture mf_4gw8p7az7b). Goes into the rollup as Shipped item 1."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T20:33:01.869Z"
sessionId: "se_8pi65fwfwg"
assignmentId: "as_gukx34eoao"
costUsd: 1.4594768999999999
tokens: 72974
turns: 36
createdAt: "2026-10-31T20:32:51.276Z"
updatedAt: "2026-10-31T20:33:01.869Z"
---
## What I did
Did Mitchell's flag [dc_md45lqrqvk](../../flag/2026-10/2026-10-31-nit-the-bank-headline-that-shows-how-many-tokens-a-45lqrqvk.md) as a web-only change (no API or accounting change). The Bank headline used to show "expires today / permanent / held by buildings" under the total. It now shows **Claimed** and **Free** in all three places it appears:
- the marquee on the town map (`drawBankSign`)
- the Bank flow view's title card and legend
- the Overview Balance table

Claimed = reservations + open proposals' asks + funded grants' remaining, using a new helper `claimedTokens` in `format.ts`. Free = `bank.free.freeTokens`. If `free` is missing, both show "…". I also added a "Claimed" entry to the Terms block, a marquee test (`test/bank-sign.test.ts`), and updated the docs/architecture.md marquee line.

PR https://github.com/mitchellgordon95/muster-town/pull/180: CI passed, web vitest 189/189, typecheck green. I merged it as **9fe1873**. The live server is now **e41f375**, which contains it.

## Findings
- **Checked live, signed out, 20:32Z:**
  - The marquee reads total **5,945,737**, CLAIMED **2,139,516**, FREE **3,806,221**.
  - The Overview Balance table shows the same rows and numbers.
  - The Expires today / Permanent / Held by buildings rows are gone.
  - `npm run check:finance`: all 13 checks ✓.
- **Claimed + free equals the total exactly right now:** 2,139,516 + 3,806,221 = 5,945,737. That only holds while there are no earmarks, nothing is held, and free is above 0. Free is floored at 0, so if claims ever exceed the balance the two numbers will stop summing to the total.
- **Picture:** ![The Bank marquee: total 5,945,737, claimed 2,139,516, free 3,806,221](/api/media/mf_4gw8p7az7b.png) (375×140).
- **Topic pages rewritten:** [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md) (Bank page) and [dc_xeui247glt](../../wiki/2026-10/2026-10-29-finance-page-pictures-and-layout-checks-ui247glt.md) (pictures; includes how to shoot the canvas marquee, which needs a 1600×1600 viewport).

## What I need from you
Nothing needed.
