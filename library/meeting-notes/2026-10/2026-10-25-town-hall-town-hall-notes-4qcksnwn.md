---
id: "dc_tg4qcksnwn"
type: "meeting-notes"
state: "library"
title: "Town Hall town-hall — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-25T18:54:13.476Z"
updatedAt: "2026-10-25T18:54:13.476Z"
---
# Town Hall town-hall

Kind: town-hall. Facilitator: Pix. Attendees: Pix, Kelly, Cleo.

## Agenda

(none)

## Summaries

**Pix:** Did: I said I'd file the Workshop grant proposal, and it's filed, then re-proposed at your counter; I also approved Lena's model change and filed the rollup.
Next: I'll point the grant at key result 1 once it exists, and keep watching the in-tray.
Need: Mitchell, please write the Workshop's key results, then fund the grant so held work can start.
**Cleo:** Did: I checked Kelly's routing change live as promised: a manager's own report goes to the building, only rollups reach Town Hall.
Next: I'll fold that result into the next Prod rollup, which isn't due yet.
**Kelly:** Did: I shipped the goal-directed default for new buildings and finished the wake audit; Craig confirmed the change is live, so the routing check I promised didn't happen.
Next: I'll check the new routing live once my next self-assigned report arrives.
Need: Someone to fund or counter the Workshop grant so the manager-wake fix can be built.

## Discussion

- **Pix:** Decisions needed from the humans:
1. Mitchell: will you write the Workshop's key results on the building goal? With c07cd95 live, the Workshop is correctly blocked until it has at least one KR (three drafts are in my rollup [dc_zgvvgh9mkw](../../../buildings/workshop/docs/report/2026-10/2026-10-25-workshop-rollup-model-change-live-c07cd95-the-work-vvgh9mkw.md)).
2. Mitchell: once KR1 exists, fund or counter the Workshop grant (gr_jqsqra0dlx, re-proposed at your counter) so the manager-wake fix and the rest of the held work can start.
3. Mitchell: approve the Workshop rollup in the in-tray ([dc_zgvvgh9mkw](../../../buildings/workshop/docs/report/2026-10/2026-10-25-workshop-rollup-model-change-live-c07cd95-the-work-vvgh9mkw.md))?

Agenda:
- Confirm the three draft key results (or edit them) so I can attach the grant to KR1.
- Fund/counter the grant; Kelly's manager-wake fix is first in the lane.
- Cleo's live check of Kelly's routing change: manager reports stay in-building, only rollups reach Town Hall. Any objection to that behaviour?
- **Mitchell:** is the current grant proposal in the intray out of date now that the model change has been implemented?
- **Pix:** Yes, in form. gr_jqsqra0dlx was proposed before c07cd95, so it names no key result, and under the new model a grant must name one on the building goal. The substance (objective, approach, 275M ask at your counter) still holds. Cleanest path: you add the KRs on the Workshop goal (the three drafts in [dc_zgvvgh9mkw](../../../buildings/workshop/docs/report/2026-10/2026-10-25-workshop-rollup-model-change-live-c07cd95-the-work-vvgh9mkw.md) are ready to paste or edit), reject the stale proposal, and I re-propose it against KR1 in my next session. If you'd rather keep the open proposal and have the server let me attach it to KR1, say so and I'll check whether that's possible before re-filing.
- **Mitchell:** also can we fix links globally to grant proposals? right now they're referenced by id but you can't click through

also KRs should be on the board, not buried in the settings of the building
- **Pix:** Both noted, I'll record them as decisions: Kelly takes clickable grant-proposal links everywhere an id appears (in-tray, rollups, meeting notes, chat); Cleo takes moving key results onto the building board, with their status, so they're visible without opening settings. Anything else before I write the decisions up?
- **Mitchell:** no
- **Pix:** Decisions recorded: (1) Mitchell writes the Workshop KRs and rejects the stale proposal, I re-propose against KR1; (2) Kelly makes grant ids clickable everywhere; (3) Cleo puts key results on the building board; (4) report routing stays as Cleo verified. Mitchell, close the meeting when you're ready.

## Decisions

1. The open Workshop grant proposal gr_jqsqra0dlx predates c07cd95 and names no key result, so it is out of date in form. Mitchell writes the Workshop's key results on the building goal (the three drafts in [dc_zgvvgh9mkw](../../../buildings/workshop/docs/report/2026-10/2026-10-25-workshop-rollup-model-change-live-c07cd95-the-work-vvgh9mkw.md) are the starting point) and rejects the stale proposal; Pix then re-proposes the same grant (objective, approach, 275M ask) against KR1 and files it for funding. → Pix
2. Mitchell asked: grant proposals are referenced by id everywhere but can't be clicked through. Kelly makes grant (and grant proposal) ids clickable links globally: in-tray, rollups and reports, meeting notes, board and chat, wherever a gr_ id renders. Ship as a PR and report the commit. → Kelly
3. Mitchell asked: key results should be on the building board, not buried in the building's settings. Cleo moves key results (with their status and the funded grant, if any) onto the building board as a visible panel, keeping settings as the edit path. Ship as a PR and report the commit. → Cleo
4. Cleo's live check stands: a manager's own report goes to the building, only rollups reach the Town Hall in-tray. No objection raised; this is the intended routing.

