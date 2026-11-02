---
id: "dc_jwwdam5oe3"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T17:28:08.835Z"
updatedAt: "2026-10-31T17:28:08.835Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** I'd like to talk about your report "Workshop rollup 34: goal tree sheet, buildings as a thin layer on goals (#152-#163), desk deaths fixed; all live on fa7…" ([dc_hlru34k0sh](../../report/2026-10/2026-10-31-workshop-rollup-34-goal-tree-sheet-buildings-as-a-ru34k0sh.md)). (presented: [Workshop rollup 34: goal tree sheet, buildings as a thin layer on goals (#152-#163), desk deaths fixed; all live on fa73e88](../../report/2026-10/2026-10-31-workshop-rollup-34-goal-tree-sheet-buildings-as-a-ru34k0sh.md))
- **Pix:** Hi Mitchell. I've got rollup 34 open. Three things shipped: the goal tree as a sheet over the map (#152), buildings as a thin layer on goals (#154-#163, migration 065 moved the three pools onto their goals), and the desk-death fix (#149). Two things I asked you for: save the collective defaults once at Town Hall → Settings, and decide on the two idle grants gr_iq5m7dug56 and gr_tvt32g9xly. What would you like to go through?
- **Mitchell:** i saved the town settings. i can't touch the grants, i guess because they didn't mark themselves as completed?
- **Pix:** Thanks for saving the settings. On the grants: close, not completion, is the catch. A human's Continue / Adjust / Cut buttons only appear when a grant hits its 100% checkpoint (web GrantRow, Places.tsx:412); neither has, they sit at 98% and 91% with no spend since 10-27. What a funded grant does show you is one "Close grant" button in the grant panel, but it stays greyed until you type something in the Note field ("the evidence the work is done"), so it looks untouchable. Two ways out: (a) I close both myself now with close_grant (the manager's early close): gr_iq5m7dug56 with steps 1-4 live as the evidence and step 5 ("0 unexpected deaths for 7 days") noted as unmet, gr_tvt32g9xly as not started; unspent tokens go back to the Bank and you mark each key result met or missed from the in-tray. (b) I queue a small change so a funded grant also shows you Cut without waiting for the checkpoint. I'd do (a) now and (b) as well if you want it. Say the word.
- **Mitchell:** oh, the greyed out button was confusing me

and sorry, what are these grants for?
- **Pix:** Both are from last week, before the goal tree existed. gr_iq5m7dug56 (1.67M tokens, 98% spent) is "the Bank counts adjusted output tokens": the five steps that made the Bank bill sessions by adjusted tokens, learn the subscription cap from the first cap death and hold work before it, all live since 10-27. The one unfinished bit is a 7-day watch of "0 unexpected desk deaths", and the desk-death fix in this rollup resets that clock anyway. gr_tvt32g9xly (300k, 91% spent) is "a member with no admin role funds a proposal from their own Bank input": the code is live (the Fund form has a "Pay from" select, and sessions run on the funder's input), but the end-to-end proof needs a second signed-in person with their own small API-key input, which the town has never had. So: the first one is done except a watch, the second is built but unproven. My suggestion: I close both now as done, with those notes; you mark the first met and the second met or missed as you see fit, and if the member-funding proof matters to you we test it when a real second member turns up. OK?
- **Mitchell:** yeah close both please. also make the close grant button enabled even if there's no note please
- **Pix:** Done. Both grants are closed as done: 26,630 and 28,100 unspent tokens went back to the Bank, and their key results now show in your in-tray with "Mark key result met" / "Mark missed" (those buttons work without a note). The button change is queued as as_h8arrmelsd: Close grant enabled with an empty note, the note optional, a blank one gets a default evidence line. It'll land in the next rollup with the commit. Anything else on 34?

## Decisions

1. Close both idle grants as done: gr_iq5m7dug56 (Bank counts adjusted tokens; steps 1-5 live, 7-day death watch unmet) and gr_tvt32g9xly (member funding built, unproven without a second member). Done by Pix in this 1:1 with close_grant; 26,630 + 28,100 unspent tokens back to the Bank; Mitchell marks kr_vyrhhiyotb and kr_6f9c200vsx met or missed from the in-tray.
2. Grant panel: the "Close grant" button on a funded grant is enabled with an empty note (the note stays optional; a blank one gets a default evidence line). Queued as as_h8arrmelsd on the Workshop queue.

