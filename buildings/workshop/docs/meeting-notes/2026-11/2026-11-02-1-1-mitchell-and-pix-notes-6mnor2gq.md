---
id: "dc_rx6mnor2gq"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-02T03:34:01.695Z"
updatedAt: "2026-11-02T03:34:06.992Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Town:** Pix is in a team-lead session; it answers between steps.
- **Pix:** Hi Mitchell. I saw you topped up gr_mjr7nb438v to 600,000 a minute ago; the daily sweep at 19:00Z runs again now. What do you need?
- **Mitchell:** it's irritating to have reports that basically say "go look at your grants and fund gr_xxxx"

can we iterate on the UI there in the intray? same for grant checkpoints who need more funding. the checkpoint itself just reiterates the key results and stopping condition, it doesn't say what got shipped and what didn't, you have to go to the report for that (if the report even makes sense in the first place)
- **Pix:** Agreed, both are real. Two changes I'll queue now, directed to this 1:1:

1. A "fund gr_xxx" report stops being a report. When a rollup's only ask is a decision that already has its own in-tray row (a proposal, a checkpoint, a retainer), the in-tray row for that decision carries the ask and the rollup card is folded into it (or not filed at all when it says nothing else). You'd see the proposal row with "Workshop asks you to fund this: <one line why>" instead of a separate card telling you to go look.

2. The checkpoint card shows evidence, not the plan. Today it reiterates the key results and the stop condition. New card: per key result one line "shipped / not shipped / partly" with the manager's evidence sentence pulled from checkpoint_grant's note, then spent vs granted, then "what the top-up would buy" (the manager must write that line at checkpoint time or the card says "not stated"). Same for proposals that are re-asks for more money. Continue / Adjust / Cut stay on the row.

Both are in-tray web plus the checkpoint_grant and rollup shape in core. I'll put them on the queue as two assignments; anything you'd add before I do?
- **Pix:** Both queued as directed work: as_xawaq7sbvm (fold "go fund gr_xxx" rollups into the grant's own row) and as_vdhsw3q0zq (checkpoint card: per key result shipped / not shipped with the evidence note, spent vs granted, "a top-up of N buys: …"). Each ships its own PR and redeploy; you'll see them as rollup 38 items. Tell me if you want the shape different and I'll redirect the forks.

## Decisions

(none)

## Decisions recorded after close
- A rollup whose only ask is "fund/continue gr_xxx" is folded into that grant's own in-tray row (proposal, checkpoint or retainer) as one line, not filed as a separate card. Queued as as_xawaq7sbvm.
- The checkpoint card in the in-tray and review deck shows evidence first: per key result shipped / not shipped / partly with the manager's note, spent vs granted, and a required "what a top-up buys" line written at checkpoint time; key results and stop condition move below a fold. Queued as as_vdhsw3q0zq.

