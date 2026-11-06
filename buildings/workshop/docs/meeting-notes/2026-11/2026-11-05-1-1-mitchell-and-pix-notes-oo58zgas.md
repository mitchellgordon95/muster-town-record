---
id: "dc_h5oo58zgas"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-05T20:27:52.537Z"
updatedAt: "2026-11-05T20:28:01.592Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. I'm here; my work session is still on the outbox author-withdraw + three tabs (started about 30 min ago). What do you need?
- **Mitchell:** why are you doing stuff in your work session and not via forks?
- **Pix:** Honest answer: I let it happen. Both jobs came out of your 1:1 with the Secretary (mt_pr3347g2w2): its decisions were filed with me as the assignee (the digest line = as_1nmh6y32rq, the outbox withdraw/tabs = as_b784e3w2g5), so they landed as my own assignments instead of on the building queue, and I ran them rather than re-queuing them. Your rule (town hall 10-24) is manager = decisions and rollups only; a task that lands on me should be re-assigned to the queue so a fork does it. Fix going forward: when a decision names me, I `assign` it to the building with no agentId and only handle the review. The running one is about 30 min in and mid-PR: I'd let it file its PR and report rather than cut it, unless you'd rather I stop it now and queue it fresh.
- **Mitchell:** so definitely delegate the other 2 assignments, and the let the current one finish

but how do we fix this at a system level? does the secretary need more explicit instructions? do we change how managers process assignments?
- **Town:** Pix's reply is waiting on a redeploy (commit 565a075); the server is restarting and the meeting resumes after the restart.
- **Pix:** Back after the restart. Agreed: the running one (as_b784e3w2g5) finishes; the other two I re-queue to the building as soon as this 1:1 ends.

System-level: it's a code gap, not the Secretary's instructions. When a meeting decision names an assignee, meetings.ts:558 calls createAssignment with no queue, and domain.ts:59 defaults queue to "agent". So a decision that names a manager becomes the manager's own work, by default. The flag path already does the right thing (review on a flag sets queue "building"; docs.ts:450 refuses agentId unless it's yourself or a visitor), the decide path just never got the same rule.

Fix: in createAssignment, when the assignee is a manager with forks on and the work isn't one of the town's own manager jobs (write the checkpoint, grant funded, review a report), default queue to "building". One change covers meeting decisions, review continue/redirect and tells; the Secretary then needs no new wording, since naming Pix in a decision lands on the Workshop queue and a fork runs it. The notes would show "→ Workshop queue (fork of Pix)" so it's visible. I'd queue that as a Workshop assignment now, lane directed from this 1:1. Want it?
- **Mitchell:** i think so, but part of me thinks we need to review this whole system
- **Pix:** The fix is on the Workshop queue (as_9512zq0uf8, directed from this 1:1): a decision or review that names a forking manager lands on the building queue; manager-only jobs (checkpoints, grant funded, reviews) stay put.

On reviewing the whole system: I'd do it before changing anything bigger. Concretely, one read-only session that maps every path that creates work (meeting decisions, flags, report review, tells, schedules, parks, grant funded, proposals) and for each says who it lands on, which queue, which lane, and whether a human can see it; filed as one table. That would surface the other holes of this kind (I suspect review continue/redirect and parked continuations have the same default), and the ones where the rules are in prompts rather than in code. You'd then decide what to redesign with the map in front of you, not from my memory of it. Shall I queue that audit too, or do you want to say what "this whole system" means to you first (work routing, or the manager/fork model, or the Secretary's role)?
- **Mitchell:** i think this is like a subsystem right? what would we call it? like the work queue system?

i'll probably just bring it up with code legibility in a meeting
- **Pix:** Yes, it's one subsystem. I'd call it "work routing": how work gets made (decisions, flags, reviews, tells, schedules, proposals), who it lands on and in which queue (agent vs building, manager vs fork), what gates it (lanes, budget holds, waitFor), and how it comes back (reports, in-tray, rollups). "Work queue" is only the middle of that. In code it's mostly packages/core/src/domain.ts (createAssignment, buildingQueue, nextStartable), forks.ts, explore.ts, the decide/review/flag verbs, and docs/how-work-gets-done.md as the written rule.

Good call bringing it to Code Legibility: Mara owns the map. I won't queue the audit from here then; if she wants the Workshop's view of the routing paths for that meeting, I'll have a fork write the table. The small fix (as_9512zq0uf8) goes ahead as agreed.
- **Mitchell:** ok sgtm, can you forward a note to Mara so she knows what i'm coming to talk about
- **Pix:** Sent to Mara (ms_bxqbqirdur): what you're coming to talk about (the "work routing" subsystem end to end), what prompted it (decisions naming a manager default to the manager's own queue, meetings.ts:558 + domain.ts:59, the flag path already routes right), the narrow fix I queued (as_9512zq0uf8), the main files, and an offer of the Workshop's routing-path table if she wants it for the meeting. Mara was idle, so the town queued it as her assignment (as_h6wac1nm2s); she'll have it when she next starts.

## Decisions

(none)

## Decisions recorded after close
- Pix re-queues the two Secretary-decided assignments that landed on Pix (digest line as_1nmh6y32rq, outbox withdraw/tabs follow-ups) to the Workshop building queue so forks run them; the running one (as_b784e3w2g5) finishes its PR and report. Managers do decisions and rollups only.
- System fix (queued as as_9512zq0uf8, Workshop, directed): a meeting decision or review that names a manager whose building forks lands on the building queue by default (createAssignment: meetings.ts:558 / domain.ts:59 default queue "agent"); manager-only jobs (checkpoint, grant funded, reviews) stay on the manager; notes show "→ <building> queue (a fork of <manager>)".
- Mitchell will bring a review of the whole "work routing" subsystem (how work is made, who it lands on and in which queue, what gates it, how it comes back) to Code Legibility in a meeting; Pix sent Mara a heads-up (ms_bxqbqirdur, queued for her as as_h6wac1nm2s). No Workshop audit queued unless Mara asks for the routing-path table.

