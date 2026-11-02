---
id: "dc_3ttdmw2wtt"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Mara — notes"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-29T04:01:10.576Z"
updatedAt: "2026-10-29T04:01:14.419Z"
---
# 1:1: Mitchell and Mara

Kind: one-on-one. Facilitator: Mara. Attendees: Mara. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** I'd like to talk about your report "Rollup: gr_x5gnnmo7yi cut taken in; gr_75eq6h3ltp (fast check) running in 4 chained steps; two new key results under "B…" ([dc_4vjinm0i7y](../../report/2026-10/2026-10-29-rollup-gr-x5gnnmo7yi-cut-taken-in-gr-75eq6h3ltp-fa-jinm0i7y.md)). (presented: [Rollup: gr_x5gnnmo7yi cut taken in; gr_75eq6h3ltp (fast check) running in 4 chained steps; two new key results under "Build times" listed for your keep/cut](../../report/2026-10/2026-10-29-rollup-gr-x5gnnmo7yi-cut-taken-in-gr-75eq6h3ltp-fa-jinm0i7y.md))
- **Mara:** Hi Mitchell. I've got the rollup open. Short version of where we stand: nothing new shipped since PR #72; you cut gr_x5gnnmo7yi and funded gr_75eq6h3ltp (120k, fast check), which runs as four chained steps. Finn is on step 1 now, timing each check step on his desk cold and after a one-file change; steps 2 and 3 (root `npm run check` with a timing line, incremental tsc, vitest --changed, then PR #71's hook as opt-in) follow, and I verify and close in step 4. The two new key results under "Build times" (Fast kr_939kp3vjxc, Observable kr_8wilbokqcn) are listed for your keep/cut; Observable has no grant yet, I'd propose one once step 1's numbers say what to measure. What did you want to go over?
- **Mitchell:** this report is the old style report, i think? do you know why you didn't use the new format?
- **Mara:** You're right, it's half-way. It has the four headings (Shipped, Decided, Key results, Needs), so the code accepted it, but Shipped is a paragraph of status instead of numbered items with **What it is:** / **What you'd see:** / **Your call:**, so the in-tray showed plain text instead of cards. Why: nothing had shipped since the checkpoint, so I wrote what changed (your cut, the new objective, the funded grant) as prose rather than forcing it into a "Shipped" item. That was the wrong call; the format exists so you can scan it, and the grant status belongs in the Key results table, not in Shipped. From the next rollup on: Shipped is either labelled numbered items or the single line "Nothing shipped since dc_…", with everything else in the table and Decided. If you'd rather I still make a labelled card for in-progress work (What you'd see: nothing yet, Your call: none), say so and I'll do that instead.
- **Mitchell:** oh i see, i was having trouble understanding what the report was saying

basically you wrote 2 key results and then wrote a report about it?
- **Mara:** Close, but the order is the other way round. At our 1:1 (mt_cy04ix9cc3) you set the "Build times" objective, and I wrote the two key results under it: Fast and Observable. Then you funded gr_75eq6h3ltp for Fast. The rollup was due because two reports got decided after that: the town notice that you cut gr_x5gnnmo7yi, and my own report cutting the new grant into four steps. So the report's job was just: (1) here's what got decided, (2) the Fast grant is running, step 1 is Finn measuring, (3) the two key results I wrote are listed at the bottom for you to keep or cut (the town appends that section for you). No work product in it, which is why it read as noise. Going forward, if the only thing to say is "work in progress, nothing to decide", I'd rather hold the rollup until there's a number or a change you can see, unless you want one every 24 h regardless.
- **Mitchell:** yeah, there's no reason to tell me that you started but have not yet completed the thing that i told you to do

and similarly no need to inform me about key results. i told you very clearly to write them, why would i want to get a report allowing me to decide again?
- **Mara:** Agreed on both. New rule for this building: a rollup only when something shipped you can see, a grant closes or hits its checkpoint, or there's something only you can give. "Started, not finished" and "I did what you told me" are not rollups. One note on the key-results block: the town appends "Key results I wrote (keep or cut)" to a manager's next rollup automatically, so that part isn't something I can leave out; but I also repeated it in prose, which I'll stop. If you'd rather the automatic block go away too, that's a Workshop change (Pix's code); I can tell Pix, or you can mention it to him directly. I'll record the rollup rule as the decision here.
- **Mitchell:** i think we need a broader UX push around goals and key results, for now just leave it alone
- **Mara:** Understood. I'll leave the goals and key-results UX alone, not raise the keep/cut block with Pix, and not write anything up about it. The only thing I change is on my side: rollups only when there's something shipped, closed or needed from you. Next one you'll see from this building is when Finn's `npm run check` with the timing line lands, with the desk numbers in it.

## Decisions

1. Code Legibility rollups only when something shipped that Mitchell can see, a grant closes or reaches its checkpoint, or a need only Mitchell can meet. No rollup for work started but not finished, and no prose restating key results Mitchell asked Mara to write (the town's automatic keep/cut block is a Workshop matter).

## Decisions recorded after close
- Goals and key-results UX (including the automatic "Key results I wrote" keep/cut block on rollups) is left alone for now; Mitchell sees it as part of a broader UX push later. Mara does not raise it with Pix or write it up.

