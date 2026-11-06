---
id: "dc_kctwnfenaw"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-05T20:54:21.831Z"
updatedAt: "2026-11-05T20:54:21.831Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Town:** Pix is in a team-lead session; it answers between steps.
- **Pix:** Hi Mitchell. I'm mid in-tray: just withdrew Pix 1's re-proposal of the "since you were last here" grant (same plan you rejected yesterday), Grant D (Town health tab, gr_8bxoy2heif, 150k) is in your in-tray, and rollup 49 is next. What do you need?
- **Mitchell:** i forgot to ask one thing from our previous 1:1

when the refactoring happens for the grant work, what happens to inflight grants (proposed and checkpointed)
- **Pix:** Short answer: nothing in flight gets touched or re-filed; each piece only applies to what starts after it lands.

- A (stable fork prompt): only changes how a session's prompt is built. Grants, proposals and checkpoints don't know about it.
- B (steps on the proposal): an already-proposed grant has no steps, so when you fund it, it takes today's path (a kickoff session on the manager). Only proposals filed after B carry steps; a countered one that gets re-proposed after B picks them up then.
- C (self-assembling checkpoint + reserve): a grant already held at 100% stays held until you continue/adjust/cut it, exactly as now. A funded grant still running starts getting fork-written KR evidence from the day C lands; whatever was spent before is just not annotated. The "fire at total minus reserve" applies to grants that haven't hit their checkpoint yet; the manager checkpoint session stays as the fallback when forks wrote nothing.
- D (health tab) is read-only.

No migration of grant rows, no re-proposing. I'll put that in B and C's proposals as an explicit line ("in-flight grants keep the current path") so it's a key result you can check, not a promise. Want me to also have B's funded path run the kickoff for old-style proposals, or leave them as they are?
- **Mitchell:** seems like this change breaks existing proposals that don't have steps baked in? and i don't want to maintain the old code paths as a fallback
- **Pix:** Agreed: no fallback paths. Then the cutover is a one-time data back-fill, not old code kept alive:

- B: the PR ships a migration that gives every open proposal (proposed or countered) one step, "Step 1: <its objective>, as in the approach", so funding it queues that step on the building queue like a new-style one. The kickoff session code is deleted in the same PR. Funded grants already past kickoff don't care. Nothing for you to re-decide; the ~6 fund asks in your in-tray just gain a "Steps: 1" line.
- C: the manager checkpoint session is deleted too. A grant already held at 100% stays as it is (its card exists, waiting on you). For grants that hit the checkpoint after C, the card assembles from what forks wrote; if no fork wrote anything, the card says "no evidence filed by the forks" and the top-up line is empty, rather than spinning up a manager session to fill it. The reserve applies to every funded grant from the day C lands, including ones mid-flight.

I'll write both into the B and C proposals as key results ("kickoff path gone", "manager checkpoint session gone", "open proposals back-filled"). OK?
- **Town:** Pix's reply is waiting on a redeploy (commit edd5da0); the server is restarting and the meeting resumes after the restart.
- **Pix:** Back after the restart (edd5da0 is live). My answer above stands: no fallback code; B back-fills every open proposal with one step and deletes the kickoff session, C deletes the manager checkpoint session and assembles the card from what forks wrote (empty evidence shown as such). If that's a yes, I'll have the B and C proposals filed with those three key results.
- **Mitchell:** ok sgtm
- **Pix:** Good. Recorded as a decision here: no fallback code paths; B's PR back-fills every open proposal with one step and deletes the kickoff session; C's PR deletes the manager checkpoint session, the card assembles from fork-written evidence (shown empty when none), the reserve applies to every funded grant from day one. Those become key results on the B and C proposals, which get scoped once A closes, as agreed earlier. Nothing in your in-tray needs re-deciding.

## Decisions

1. Grant-work refactor cutover (Mitchell: "ok sgtm"): no old code paths kept as fallbacks. Grant B (steps on the proposal): its PR ships a migration that back-fills every open proposal (proposed or countered) with one step "Step 1: <objective>, as in the approach" so funding queues it on the building queue, and deletes the manager kickoff session. Grant C (self-assembling checkpoint + reserve): its PR deletes the manager checkpoint session; the checkpoint card assembles from fork-written KR evidence and shows "no evidence filed by the forks" when there is none; a grant already held at 100% stays held as is; the reserve applies to every funded grant from the day C lands. These are key results on the B and C proposals (scoped after grant A closes, per mt_o0exccdv8g). Nothing in flight is re-filed or re-decided.

