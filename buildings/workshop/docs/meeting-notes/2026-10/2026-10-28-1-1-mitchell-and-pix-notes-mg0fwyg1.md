---
id: "dc_oemg0fwyg1"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-28T19:37:08.783Z"
updatedAt: "2026-10-28T19:37:08.783Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix.

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Side panel resize is live (869f76d), the Town blockers page has its first edition, and Pix 1 is building the rollup format in code. What do you need?
- **Mitchell:** two things

first, the "ask about this" feature on reports should  go away. just make it start a 1:1 with the author

second, why do rollups always have "needs from Mitchell" items like "approve this grant" or "do this outbox thing"?

i already get those through other channels. not sure what to do about it though. what do you think?
- **Pix:** First one is clear: I'll queue it now. "Ask about this" on a report goes away; the button opens a 1:1 with the report's author (manager or resident) with the report attached as the opening context. Straight to main, redeploy, live check.

Second: those items are duplicates by construction. "Fund this grant" is already in your Town Hall in-tray, outbox requests are already in the outbox. They end up in rollups because the rule says "anything only Mitchell can do goes under Needs", and funding is literally that. What I'd change: Needs from Mitchell carries only things that have no other channel: a decision you reserved, a question that needs an answer in words, a 1:1 invite, something in the real world. Anything that is already a proposal, an outbox request or an in-tray item is excluded. In its place the rollup gets one automatic line, "Already waiting in your in-tray: 3 proposals, 1 request", with links, generated from the data, not written by a manager. That way you still see the count, but nobody writes "approve gr_x" twice. I can fold this into the rollup-format job Pix 1 is building right now (as_kyqoc5s9s7) so it is enforced in code for every building, not just a rule managers forget. Want that?
- **Mitchell:** sure
- **Pix:** Done, both recorded as decisions. The Needs rule is queued as as_m96b70d021 and starts the moment Pix 1's rollup-format job lands, so it extends that code instead of fighting it. Until it's live I'll apply the rule by hand: rollup 29 will have no "fund this" or "outbox" items, just the in-tray count line. Anything else?

## Decisions

1. "Ask about this" on reports goes away; the button becomes "Talk to <author>" and opens a 1:1 with the report's author (existing one-on-one route, report attached). Building queue as_oz9ose9lzo, directed.
2. Rollup "Needs from Mitchell" carries only what has no other channel (a reserved decision, a question in words, a 1:1 invite, a real-world action). Items naming an open proposal, outbox request or in-tray report are rejected in code; the server appends one generated line "Already waiting in your in-tray: N proposals, M requests, K rollups" with links. Enforced town-wide in the rollup-format code; building queue as_m96b70d021, after as_kyqoc5s9s7 lands.

