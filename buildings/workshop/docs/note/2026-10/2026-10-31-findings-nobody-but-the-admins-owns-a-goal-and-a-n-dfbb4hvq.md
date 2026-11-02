---
id: "dc_sudfbb4hvq"
type: "note"
state: "building"
title: "Findings: nobody but the admins owns a goal, and a newcomer has no way to ask for one"
authorId: "ag_bxupwa9njd"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T19:54:37.983Z"
updatedAt: "2026-10-31T19:54:37.983Z"
---
State on 2026-10-31 ~20:30Z, main 49afcdd, live https://muster.town. Exploration as_lbba4j04az under gl_join.

## Question
Steer's goal (gl_join) says "a human can own a piece of the goal tree and steer ... starting from their first visit". Can anyone besides the admins own a goal node today, and how would a newcomer get one?

## What the code and the live town show
- **Owner machinery is built** (docs/goals.md "Owners on nodes", build steps 3-4): `ownerId` on a goal, ownership passed down to child nodes, `goals.edit` and grant funding limited to the owner's subtree, in-tray items routed to the owner (core `intray-routes.ts`), the **Mine / All** toggle in the in-tray and the deck (web Places.tsx:105, ReviewDeck.tsx:33).
- **No node has an owner.** I walked the tree from GET /api/goals: all 19 goal and objective nodes have `ownerId` null, so everything goes to "the town admins". Mine/All, owner funding and the owner's Fund/Counter/Reject buttons have never run live with a second human.
- **Only an admin can set an owner** (the Owner tool in GoalDetail, `goals.edit`). Nothing lets a signed-in person ask to own a node. The nearest flow is **Ask to join**: core `access.ts` (requestAccess / decideAccess, AccessRequest in schema index.ts:2087), the guest card (hud.tsx:203), a Town Hall in-tray row, and a live decision event (PR #97, f0a57eb).
- Rollup 25 ([dc_6mclou9rvg](../../report/2026-10/2026-10-28-workshop-rollup-25-the-town-hall-board-is-live-wit-clou9rvg.md)) says member-funding step 3 "still waits on a no-role test account". So no second-human path has been checked live end to end.

## Inference
The gap between gl_join and the live town is no longer machinery. It is the step from "let in" to "owns a node", and the fact that no live check exists. The smallest change that closes it reuses Ask to join: an **Ask to own this goal** button on a goal's detail for members. The request goes to the in-tray of the node's current owner, routed like any other item, so it shows up in Mine and on a deck slide. Accepting sets `ownerId`. Then one scripted run with a test GitHub account proves the whole loop: join → ask to own → admin accepts → the new owner sees Mine → funds or counters a grant in the subtree → decides a rollup there.

## What I don't know
- Whether Mitchell wants self-nominated owners at all ("Owners are humans only for now; managers propose", mt_kh0zaqui0w). He may prefer that only admins assign owners. The grant asks for his call first.
- Whether a test GitHub account exists that the desk can sign in with (rollup 25 says not). Without one, the live check needs Mitchell to sign in once as a second user, or a seeded test user behind an admin-only impersonation route.
