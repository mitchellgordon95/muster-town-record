---
id: "dc_w2exk7u74j"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T22:21:01.483Z"
updatedAt: "2026-10-31T22:21:08.250Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Live is ae18eb3 (the 503 post-mortem and the Bank.debited fix), rollup 35 is in your in-tray, and PR #214 (onboarding lag script) is waiting on CI. What do you need?
- **Mitchell:** so weird thing happened, your former teammates all respawned. might have been a server restart thing? idk, but there's no buttons to dismiss them now

also i urgently need an operational budget reserve of like 500k. so that way even if grants and exploration burn through the rest, i can still do 1:1s and stuff
- **Pix:** Two things, both on it.

1. Respawned residents. In the code a dismissed agent keeps its row with status "retired" and the web client never draws it (state.ts drops it on sight). So they are back because something flipped their status, not because the rows were recreated. I can't see the live DB from here; I'm queuing a fork to read the event log around the last restarts for the agent.retired rows and whatever status change followed, fix the cause, and re-dismiss them. The Dismiss button was cut with the resident management UI in PR #101; DELETE /api/agents/:id still works, so the fork puts an admin-only Dismiss back on the agent panel.

2. Operating reserve. Today free tokens = Bank balance minus funded grants' remaining, open asks and reservations. Plan: a town setting "operating reserve" (500,000 now, editable on the Bank page), subtracted from that general balance before anything is counted free. Exploration ticks and grant funding can't reach it (funding a grant that would dip into it is refused with a message saying so); 1:1s, meetings, manage sessions and directed work draw past it as normal. The Bank shows the reserve and what is left above it. Queuing it now as directed work from this 1:1, ask-first rule satisfied since you asked.

One check: should the reserve also stop a human from funding a grant, or only the agents (explorers and proposals)? I'll go with both unless you say otherwise.
- **Town:** Pix's reply is waiting on a redeploy (commit ae18eb3); the server is restarting and the meeting resumes after the restart.
- **Mitchell:** can you even queue work with all your desks blocked?
- **Pix:** Yes, queuing works: the operating reserve assignment went on the Workshop queue about a minute before the restart (as_rsosm2rfau, pending). What I can't see from here is whether a fork can start on it. Live forks are 0 and two assignments have sat pending since the restart, so either the scheduler hasn't ticked yet or the four respawned bodies (Root, Sage, Keel, Lena, all "idle" in the Workshop right now) are holding the desk slots. The respawn fix is going on the queue now and I'll ask it to free the desks first: nothing in the restart reconcile touches "retired" (it only flips working/walking bodies to idle), so something else rewrote their status and the fork reads the event log to find it, fixes it, re-dismisses them, and puts an admin-only Dismiss back on the agent panel. If you want them gone this minute, DELETE /api/agents/<id> with your token still dismisses one. Reserve: I'm going with "the reserve stops everyone, humans included, from funding a grant into it" unless you say otherwise.
- **Pix:** Queued: as_9nmn5fytbu (respawn fix: free the desks first, find and fix the status writer with event-log evidence, re-dismiss the four durably at startup, admin Dismiss button back) and as_rsosm2rfau (operating reserve, 500,000, editable on the Bank page, exploration and grant funding can't touch it, 1:1s and meetings draw past it). Both directed from this 1:1. Anything else, or shall I let them run?

## Decisions

(none)

## Decisions recorded after close
- Dismissed residents (Root, Sage, Keel, Lena) respawned as idle after today's restarts and hold the Workshop's desks: find what rewrote "retired", fix it, re-dismiss them durably at startup, put an admin-only Dismiss back on the agent panel. Already queued as as_9nmn5fytbu.
- Operating reserve: a town setting of 500,000 tokens (editable on the Bank page) that free tokens exclude, so exploration and grant funding (humans included, unless Mitchell says otherwise) can't dip into it, while 1:1s, meetings, manage and directed sessions draw past it. Bank change asked for by Mitchell. Already queued as as_rsosm2rfau.

