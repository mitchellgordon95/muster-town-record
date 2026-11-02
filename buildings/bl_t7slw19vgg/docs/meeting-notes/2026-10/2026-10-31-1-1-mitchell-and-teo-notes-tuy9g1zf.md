---
id: "dc_0ltuy9g1zf"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Teo — notes"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T21:04:17.441Z"
updatedAt: "2026-10-31T21:04:20.320Z"
---
# 1:1: Mitchell and Teo

Kind: one-on-one. Facilitator: Teo. Attendees: Teo. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Teo:** Hi Mitchell. Right now two forks are running: one is checking "no dead ids" live, and one is clamping map bubbles so they stay on screen. What do you need?
- **Mitchell:** i want you to keep iterating on the town organization

let's allow building entrances to be on any side of the building to allow better stacking

fountain plazas also look basically the same as the tree. i think what i really wanted for that setting is like a nicely-planned out town that actually feels like a town, you know? maybe take some screenshots and iterate until it's delightful

delightful being the key word there

we might also want to add a goal to your work of making human use of the town "delightful"
- **Teo:** Got it. Here's the plan:
1. Doors on any side. Today every door faces the road below the building. I'll let the layout put a door on whichever side faces the nearest street, so buildings can stack back to back and side by side.
2. Make "fountain" its own town. Right now it's basically the tree with fountains added. It should look planned: a central square with the Town Hall and a fountain, a main street and cross streets, building blocks along them, and trees, benches and lamps. The fork will screenshot it at 1280×720 and 390×844, look at the pictures, change things, and repeat. It doesn't stop at "works"; it stops when it looks delightful, and it posts before/after pictures.
3. A new key result under our goal: "Human use of the town is delightful". I'd make it checkable with a short list of first-visit moments (the map, opening a building, reading a report, the 1:1) that each have to feel good on desktop and on phone.
I'll queue 1 and 2 as one directed job, since they touch the same layout code, and propose 3 as a key result. Does that match what you want, or do you want doors to apply to all three layouts and not just fountain?
- **Town:** Teo's reply is waiting on a redeploy (commit 36a8a86); the server is restarting and the meeting resumes after the restart.
- **Teo:** We're back after the restart. One update: both forks finished while it was down. "No dead ids" checked out live, and bubble clamping is merged (63ed49e). My plan above still stands. Tell me whether doors on any side should apply to all three layouts or only the fountain one, and I'll queue the work.
- **Mitchell:** sgtm
- **Teo:** Done. I queued one job for a fork (as_6gd7y6u4yz). It lets doors face any side in all three layouts, rebuilds "fountain" as a planned town, and iterates on screenshots at desktop and phone size until it looks delightful. The report will have before/after pictures. I also proposed the "delightful human use" key result (gp_9j6wrqggce) for you to accept or cut. I'll report back when the layout is live.

## Decisions

(none)

## Decisions recorded after close
- Doors on any side in all three layouts; rebuild 'fountain' as a planned town; iterate on screenshots at 1280×720 and 390×844 until delightful; report with before/after pictures.
- Propose a key result under the UI / UX goal: human use of the town is delightful, checked by the first-visit moments (map, opening a building, reading a report, 1:1) on desktop and phone. Proposed as gp_9j6wrqggce.

