---
id: "dc_ri2n5ng3or"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-05T21:59:14.544Z"
updatedAt: "2026-11-05T21:59:14.544Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Live is 42edae0 (7 min ago; #372 steps-in-proposal and #373 outbox refetch fix). What do you need?
- **Mitchell:** how much of the work we discussed in that long 1:1 is done? i'm waiting to decide other grants until the paperwork is more efficient
- **Pix:** Of the four from mt_o0exccdv8g (page dc_6tkj6b32bi): roughly a quarter.
- A (fork prompt, gr_9kt5t7w51w, funded 1M): step 1 of 3 is live since 21:40Z (PR #372): fixed fork system prompt per building, live state in the first message, ~8.5k tokens vs 20.8k before (target 8k). Step 2 (the wrap-up line that caps kickoff/checkpoint sessions) and step 3 (measure, close) not started; a cache live check resumes in ~1 h.
- D (Town health tab, gr_8bxoy2heif, 150k): proposed, in your in-tray, untouched.
- B (steps in the proposal: funding queues step 1 itself, no manager kickoff session + back-fill migration) and C (checkpoint card assembles from fork evidence, no manager checkpoint session, reserve): nothing yet. We agreed to propose them after A closes.
B and C are the paperwork savers, so that sequencing is what's blocking you. I'd rather queue the scope-and-propose for B and C now (two assignments, exploration lane) and not wait for A. Say yes and they go on the queue.
- **Mitchell:** yes please
- **Pix:** Done. Two assignments on the Workshop queue, both directed from this 1:1: B scope-and-propose (as_3hdrsvyq02) and C scope-and-propose (as_yswef29vav). Each reads the code, writes the plan, and files a proposal; neither builds anything. Both carry the no-fallback cutover rule (B back-fills open proposals with one step; C leaves a grant already held at 100% as is). The two proposals should be in your in-tray within a couple of hours; C's note will flag the reserve as a Bank change for your yes. Until then, D (gr_8bxoy2heif) is the only one waiting on you.
- **Pix:** B is already in your in-tray: gr_b5fyqibfx2, 350k, five key results due 11-08/11-09 (plan [dc_lq9eo4lz5a](../../wiki/2026-11/2026-11-05-grant-b-steps-in-the-proposal-no-kickoff-session-9eo4lz5a.md)). Funding queues step 1 straight onto the building queue and deletes the kickoff session; a migration gives every open proposal one step; the next step queues itself when a step's fork reports (a pivot leaves it to me). Pix 1 picked that over "manager review continue" so no manager session runs per step. C is still being scoped.
- **Pix:** C is in your in-tray too: gr_95svkzi4l6, 450k, five key results due 11-09/11-10 (plan [dc_nqgbjho18g](../../wiki/2026-11/2026-11-05-grant-c-self-assembling-checkpoint-card-reserve-gbjho18g.md)). Pix 2 measured the cost: 18 holds at 100% since 10-31, the checkpoint session a median 108k each, about 3.33M booked past 100% over 17 grants. The plan: delete the checkpoint session (no fallback), forks file key-result evidence and the top-up line in their own submit_report, the card assembles from that, and a reserve of min(150k, a third of the grant) moves the hold point so the running fork finishes inside the grant (would have covered 5 of 7 past overruns). The hold-point change is the one Bank-adjacent piece; the note asks your yes. So your in-tray now has B, C and D from that 1:1; A is running.
- **Town:** Pix's reply is waiting on a redeploy (commit fcdb025); the server is restarting and the meeting resumes after the restart.
- **Pix:** Back after the restart (live is now fcdb025). Nothing changed on my side: B (gr_b5fyqibfx2), C (gr_95svkzi4l6) and D (gr_8bxoy2heif) are in your in-tray, A is running. If you want to fund B or C from here, say so and I'll do it in your words; otherwise end whenever you're ready.

## Decisions

1. Propose grants B (steps in the proposal, kickoff session deleted, back-fill migration) and C (self-assembling checkpoint card from fork evidence, checkpoint session deleted, reserve) now, not after A closes: scope-and-propose assignments as_3hdrsvyq02 and as_yswef29vav on the Workshop queue.

