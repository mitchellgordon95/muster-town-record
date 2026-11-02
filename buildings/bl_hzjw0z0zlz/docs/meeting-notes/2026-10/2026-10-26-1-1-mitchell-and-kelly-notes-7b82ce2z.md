---
id: "dc_4h7b82ce2z"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Kelly — notes"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-26T17:09:01.465Z"
updatedAt: "2026-10-26T17:09:01.465Z"
---
# 1:1: Mitchell and Kelly

Kind: one-on-one. Facilitator: Kelly. Attendees: Kelly.

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Kelly:** Hi Mitchell. Quick status: homepage and /workshop are live, the KR 2 first-screen PR (#57) is merged and waiting on redeploy, Craig is on PR 3 (sign-in + two-user presence). What do you need?
- **Mitchell:** i think we can keep use the help overlay is the first thing the user sees on the homepage? it's basically a pitch, right. let's think about onboarding as selling the ideas (collectively funded, publicly legible, projects you care about) and then other options like BYOA and goal oriented work

i also replied to one of your reports about style consistency, ptal
- **Kelly:** Read your reply, agreed. Here's how I'd shape it: the homepage becomes the pitch, in the overlay's visual theme. Top: three idea sections, "Collectively funded" → "Publicly legible" (watch the agents work, every doc and token visible) → "Projects you care about". Then the collectives as square tiles, each with a live preview window of its town and an Open button. Then "Other ways in": bring your own agent (BYOA) and goal-oriented work (fund a key result). The in-town overlay keeps only the "your first minute" page, since the pitch moved to the homepage. One check: do you want a scrolling page with sections, or the overlay's paged card as a modal on first visit? I'd go scrolling page, plain HTML, same theme. If you nod, I give Craig the homepage pitch + tiles as PR 4 of the stranger-path grant after PR 3, and I write the style-guide skill myself (colours, type, card/tile/button rules, copy tone) first so the PR follows it.
- **Mitchell:** uh, we can try scrolling i guess. i liked the modal a lot though
- **Kelly:** Then let's keep the modal, it's your call and it already works. Homepage: the paged card opens on top of the collectives tiles on first visit (Collectively funded → Publicly legible → Projects you care about → last page: BYOA and goal-oriented work, with a "Pick a collective" button that closes it). Dismissed once, it stays closed (localStorage), with a "How this works" link to reopen it. The tiles with live previews sit behind it, so the pitch ends by revealing the list. Same paged component as in town, so the theme matches for free. I'll record it: Craig gets the homepage pitch modal + square tiles with town previews as PR 4 of gr_cm3zha6mk6 after PR 3; I write the style-guide skill first. Anything else before I file those?
- **Mitchell:** maybe we merge the projects you care about with the actual homepage which lists the collectives?
- **Kelly:** Yes, better. So the modal is two pitch pages, Collectively funded → Publicly legible, and the third page is "Projects you care about": the actual collectives list, square tiles with live town previews, rendered inside the card. Picking a tile closes the modal and opens that collective. Behind the modal is the same tile list plus a small "Other ways in" row (BYOA, goal-oriented work), so a returning visitor who dismissed the card lands straight on the list. Recording that now unless you want to change anything.
- **Mitchell:** sgtm

## Decisions

1. Homepage becomes the pitch in the help overlay's theme: a paged modal on first visit, Collectively funded → Publicly legible → Projects you care about (the collectives list itself: square tiles with live town previews, picking one opens it). Behind it the same tiles plus an "Other ways in" row (BYOA, goal-oriented work). Dismissed once it stays closed, reopenable via "How this works". In town the overlay keeps only "Your first minute". Craig does it as PR 4 of gr_cm3zha6mk6 after PR 3. → Craig
2. Kelly writes a style-guide skill (muster-style-guide) from the overlay's theme: colours, type, tiles, buttons, copy tone, phone rules, screenshot rule; pinned for the building; PR 4 follows it. → Kelly
3. Mitchell's friends test multiplayer (real GitHub sign-in, two users) later this week; PR 3's sign-in and presence stay intact.

