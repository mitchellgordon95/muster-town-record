---
id: "dc_21ftg9m0zp"
type: "report"
state: "building"
title: "Your asks take a note now: Done, Decline, Claim and Decline on request asks all carry your words to the agent who asked (live on 57a573df)"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_x02txe8mey","dc_fyox7jmhdh","dc_wr1d5s5tax","dc_cs6me6go5r","dc_pkg3il7ajc","dc_p3c91rs2vv"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/408"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-10T18:09:28.027Z"
sessionId: "se_vrr7chibc1"
createdAt: "2026-11-10T18:09:27.999Z"
updatedAt: "2026-11-10T18:09:28.027Z"
---
Live: 57a573df (since 2026-11-10 18:07 UTC). Directed work from your 1:1 with Secretary earlier today (mt_ewxnhs90cq), including the line you added at 17:38 UTC about clicking Claim and wanting to type "use Wright's VPS".

## Shipped

**1. A note on every plain ask button: Done, Decline, Claim and Decline on request asks**

**What it is:** In the Town Hall in-tray, a click ask (Done, Decline, Add, …) now has an "Add a note" link beside its buttons. Type a line, press the button, and the words go to the manager of the building that filed the ask as an inbox message: `Mitchell decided your ask "<title>": Decline. <your note>`. An outbox-request ask's buttons now read Claim… and Decline…: Claim opens an optional note that reaches the request's author (placeholder: "how you'll do it, e.g. use Wright's VPS"), Decline opens a required one. Before this, the card's Decline sent no words and the server refused it, so Decline on a request ask failed on live. PR #408, reports [dc_x02txe8mey](2026-11-10-click-asks-take-an-optional-note-with-done-decline-2txe8mey.md), [dc_cs6me6go5r](2026-11-10-pr-408-widened-to-outbox-requests-claim-note-decli-6me6go5r.md), [dc_p3c91rs2vv](2026-11-10-57a573df-is-live-click-ask-notes-and-request-claim-c91rs2vv.md).

**What you'd see:** Town Hall in-tray, any click ask: "Add a note" under the buttons; any outbox-request ask: Claim… / Decline… with a note field. No human has used it on live yet (checked the last 500 events at 18:07 UTC), so the first message with a note will be the one you send. No crop: only a human with building.fund can decide an ask, so a fork could not photograph a real one. Asks the Town Hall files itself have no manager, so a note on them stays on the ask's record only.

**Your call:** None.

## Decided
- [dc_x02txe8mey](2026-11-10-click-asks-take-an-optional-note-with-done-decline-2txe8mey.md) → approve (PR #408: click-ask note + manager message, parked on CI)
- [dc_fyox7jmhdh](2026-11-10-message-from-mitchell-via-secretary-teo-widen-as-y-ox7jmhdh.md) → approve (your 17:38 line relayed by Secretary, folded into the same PR)
- [dc_wr1d5s5tax](2026-11-10-message-from-mitchell-via-teo-1-done-in-408-79a4fe-1d5s5tax.md) → approve (Teo 1's relay that the request-ask side was done in 79a4fed5)
- [dc_cs6me6go5r](2026-11-10-pr-408-widened-to-outbox-requests-claim-note-decli-6me6go5r.md) → approve (PR #408 widened to request Claim/Decline notes, knip fix, 414 web tests green)
- [dc_pkg3il7ajc](2026-11-10-pr-408-merged-as-57a573df-click-ask-and-request-as-g3il7ajc.md) → approve (PR #408 squash-merged as 57a573df, no redeploy, parked on its deploy)
- [dc_p3c91rs2vv](2026-11-10-57a573df-is-live-click-ask-notes-and-request-claim-c91rs2vv.md) → approve (57a573df live, strings in the live bundle, no human use yet)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_4csjpgh346 (sidebars and sheets, funded) | kr_xnt1h13yce one shared Sheet | on-track, evidence in hand (PR #371 live) | see the grant card / 1,500,000 |
| | kr_gg1wjnt07k in-tray and cabinet items in a sheet | on-track, evidence in hand (PR #374 live) | |
| | kr_sa1gn36ndz links open the link sheet | on-track, evidence in hand (PR #376 live) | |
| | kr_pm0fmsiaxs rich HTML + sandboxed page docs | on-track, evidence in hand (PR #375 live) | |
| | kr_nokx342ovj the rule in the style guide and docs/ | not-started (check scheduled 2026-11-14 10:00 UTC, sc_91et8n5w5r; due 11-16) | |

Spend today by lane (at the start of this session): exploration 0 tokens; directed 117,374 tokens (the PR #408 chain).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_irjtu6tknu), 0 requests, 0 rollups._
