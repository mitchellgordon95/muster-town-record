---
id: "dc_9gcxz43hbc"
type: "report"
state: "building"
title: "Work routing map filed for Mitchell's meeting (dc_4xww7x920l): 21 paths create work, 13 can land on a forking manager's own queue; Workshop PR #369 closes 3"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_ayegd42q8w"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/369"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-08T03:26:11.709Z"
sessionId: "se_ut1avivkfs"
createdAt: "2026-11-05T20:35:31.599Z"
updatedAt: "2026-11-08T03:26:11.709Z"
---
Live: 565a075 (nothing of ours in it; this rollup carries the map Mitchell asked for via Pix, mt_peubjyoo0k).

## Shipped
**1. The work-routing map you asked for is filed**
**What it is:** A read-only map of every path that creates work in the town (21 of them, each with file:line and the test that names it), which queue it lands on, what gates it, and how it comes back. 13 paths can put work on a forking manager's own queue instead of the building queue; the Workshop's PR #369 closes 3 (meeting decisions, decisions approving the manager's reports, review continue/redirect on the manager's own report) and leaves 10 (tell relays, mentions, request answers, amended-decision wakes, a human's `assign`/POST work naming the manager, schedules with takerId, retry, flags with assigneeId, parked own work). Also: 3 rules that exist only in prompts, 6 places where docs disagree with the code, and 6 questions a redesign would have to decide (§4). Map: [dc_4xww7x920l](../../article/2026-11/2026-11-05-work-routing-the-map-ww7x920l.md); topic page [dc_ktzj41hv8x](../../wiki/2026-11/2026-11-05-work-routing-zj41hv8x.md); report [dc_ayegd42q8w](2026-11-05-work-routing-map-filed-dc-4xww7x920l-21-paths-crea-egd42q8w.md).
**What you'd see:** Code Legibility filing cabinet → "Work routing: the map" (article). No UI change; no code changed.
**Your call:** Read §4 before the Code Legibility meeting and say whether the 10 remaining paths should be fixed one by one (Workshop PRs like #369) or the routing redesigned as a whole; the docs fixes (architecture.md diagram and table, invariants 7–8, how-work-gets-done §6) wait for that answer.

## Decided
- [dc_ayegd42q8w](2026-11-05-work-routing-map-filed-dc-4xww7x920l-21-paths-crea-egd42q8w.md) → approve (map filed; nothing to run until the meeting)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_7op2v8fjcl (red-main fixer) | step 3: 7-day observation | at checkpoint, held | 502,912 / 500,000 |
| gr_baf19xtg7p | proposed, awaiting your decision | — | — |

Spend today: exploration 64,411; directed 296,119 (this map and the heads-up session).

## Needs from Mitchell
- When you bring work routing to Code Legibility, invite me (ag_croreod6q3) to the meeting; the map's §4 lists the 6 decisions it needs from you.

_Already waiting in your in-tray: 1 proposal (gr_baf19xtg7p), 1 request (dc_bn4s4m7cq3), 0 rollups._
