---
id: "dc_ihgbot3mq8"
type: "report"
state: "building"
title: "gr_8i952perny step 2: Stop grant in the web + in-tray/deck stopped row, PR #280 (CI pending)"
authorId: "ag_mcdhzznrar"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. The continuation already runs as as_dovx2e9ta6 (Pix 2: merge #280 if green, redeploy). The throwaway grant goes to Mitchell as a proposal from me; note that stop is human-only (core grants.ts:603), so Mitchell both funds and stops it; the Bank check is a separate assignment once he has."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T03:33:07.763Z"
sessionId: "se_wycv08nfue"
assignmentId: "as_vcaxi6enhb"
costUsd: 3.2662101
tokens: 163311
turns: 16
createdAt: "2026-11-03T03:28:15.758Z"
updatedAt: "2026-11-03T03:33:07.763Z"
---
## What I did
PR #275 was still open (CI green) when I started, and Pix 1 was merging it, so I left it alone. It then landed on main as 227906a, and I merged main into my branch (f88c72d). I built step 2 and opened draft PR #280: https://github.com/mitchellgordon95/muster-town/pull/280. `npm run check` is green at my desk: docs, knip, typecheck, core 690, server 267, runtime and web tests. I updated item 21 on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) and rewrote the topic page [dc_oghes5lgud](../../wiki/2026-10/2026-10-28-grants-key-results-and-the-town-hall-in-tray-hes5lgud.md). I'm parking on {pr: 280}.

## Findings
**What #280 adds**
- **Stop grant… button.** It sits on a funded or checkpoint GrantRow, in the Town Hall in-tray and in the grant panel. It shows for a signed-in human who can fund the grant (building.fund or the goal's captain), and the reason is required. The form says what will happen before you press it.
- **Labels.** `stopping` and `stopped` get a red pill and the line "<who> stopped it: <reason>". The money line reads "spent X of Y; Z unspent returned to the Bank as free tokens", or says the rest stays on the funder's input. The Grants tab now lists `stopping` with the settled grants (before this it showed nowhere). GoalsTab and the settled lines got a `stopping` case.
- **In-tray.** GET /api/buildings/town-hall/intray now returns `stopped` (core `stoppedGrants`). That is every grant still stopping, plus those closed as stopped in the last 3 days. Withdrawn proposals are left out because they aren't stops. These grants are routed, so "Mine" shows them to the goal's captain. They are not counted in the badge, since there is nothing left to decide. The web shows them in a "Stopped: for the record" section.
- **Review deck.** Each stop gets a `stopped` slide: who, why, spent of granted, where the rest went, the key results, and "Your call: None". It is left out of slide 1's decision count.
- **My design choice:** a stop shows for 3 days instead of waiting for someone to acknowledge it. The human who stopped it would otherwise have to dismiss their own decision. Say if you want an "acknowledge" button instead.

**Evidence per key result**
- **kr_ghexd88frr:** covered by tests on main (227906a). The server test covers human 200, manager stop 403, manager close-stopped 403 and withdraw 200. It is not live-checked yet: health must contain 227906a.
- **kr_4s0ccmvtsp:** covered by the core test on main. A running fork is interrupted, the queued assignment is cancelled with the reason, and the grant goes from stopping to stopped once the session ends.
- **kr_kaz3nj127k:** the core tests pass (pool: free tokens go up by the unspent rest; member: the input stays at 460,000). The live comparison of the Bank page with GET /api/bank is not done yet.
- **kr_f46tddd9as:** the server test shows every key result missed with the note. #280 adds tests for the in-tray `stopped` list, its route and the deck slide. The live in-tray row and the picture are not done yet.

**Plan for the continuation**
1. When CI is green, merge #280 and queue a redeploy.
2. Once health contains the merge commit and a throwaway grant is funded: read GET /api/bank (free tokens) and the Bank page, stop the throwaway grant with a reason, and read both again.
3. Check GET /api/grants/<id>: every key result should be missed with "Grant stopped: <reason>", and the manager should have the system message.
4. Take a cropped picture (≤300 px) of the "Stopped: for the record" row and put it on item 21.

## What I need from you
Fund a tiny throwaway grant, under 10k tokens, that the Workshop manager proposes (agents can't fund), so the next session can stop it live and check the Bank numbers. If you'd rather not, say so and I'll close the live check on the tests alone.
