---
id: "dc_ql4dvey92b"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Secretary — notes"
authorId: "ag_7tiwyqva83"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-22T18:50:42.187Z"
updatedAt: "2026-11-22T18:50:42.187Z"
---
# 1:1: Mitchell and Secretary

Kind: one-on-one. Facilitator: Secretary. Attendees: Secretary. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Secretary:** Hi Mitchell. The queue holds 10 open asks: one click at the top (Accept the test account's captain row), then the captains grant adjust-or-cut, then eight fund cards. What do you need?
- **Mitchell:** where do i see the  captain request?
- **Secretary:** You can't, on the live build: there is no row with a button. Since the queue redesign a captain request only gets Accept/Decline through an ask aimed at it (queueOrder.ts:72-74, asks.ts:71-74). Without one it shows only as a grey line under the queue, "Captain request: its card is being written", with nothing to press (queueOrder.ts:11, DecisionQueue.tsx:143). Pix's card points at a row that no longer exists, and its own two branches do nothing to the request. Fix: I file a click ask on the request itself, branches Accept / Decline, so the Accept button on that card does the act. Pix's pointer card then comes off the queue. Say "file it" and I'll do it now.
- **Mitchell:** sure
- **Secretary:** Done. The card "Accept the test account as captain of the progressive disclosure goal" is now in your queue, aimed at the request: its Accept button accepts it. Pix's pointer card is folded into it and gone from the queue. Pix knows. Press Accept on the new card when you see it.
- **Mitchell:** for this one i think we just stop waking the secretary on a schedule? just do it after new asks are posted to the queue? or if that's too frequent then in batches of 15 minutes, we programmatically check if the queue has new items and then run the secretary?
- **Secretary:** Agreed, and the pieces mostly exist. Today I run three ways: the daily schedule (dead since Wed), a debounced run after each of your decisions (secretary.ts:248), and a 1-hour backstop for unrendered needs (secretary.ts:272). The trouble is all three are gated on the daily schedule being active and funded (secretary.ts:252, 276): when it died, everything died. Your shape: drop the schedule, add "new item in the queue → one run, batched 15 min" like the decision run, keep the backstop, and give the runs a standing per-run cap instead of a 14-day retainer. That is a different plan from Pix's 250k grant, so the right button is Counter: the Workshop rewrites the plan to your words. Say "counter it" and I'll do it quoting you, or "reject" if you'd rather I queue it as directed work to the Workshop.
- **Mitchell:** counter
- **Town:** Secretary did this for Mitchell: counter gr_mcuj10tupi ("Captain and join requests always reach a human"), now countered. Citing: "counter"
- **Secretary:** Countered, as you, at the same 250k. The note on the grant carries your words: no schedule, run the Secretary after new asks land or in 15-minute batches when the queue has new items, keep the decision run and the 1-hour backstop but ungate them from the dead schedule, standing per-run cap instead of a 14-day retainer. Pix sees it in the Workshop in-tray and re-proposes with the new plan. The card is off your queue.
- **Mitchell:** ok this is another example of the same thing over and over again

i get asked for a click somewhere in the UI. the buttons on the card should do the thing, but for some reason they can't

do we dig into the decision queue abstraction a little bit and figure out what's going on here? in my naive view, buttons should just be connected to API endpoints that get hit when the user makes a decision. do we need to provide some kind of "hooks" affordance to ask card authors?
- **Secretary:** Dug in. Your naive view is right and the code half-does it. A button acts only when the card's targetKind is one of six (grant, retainer, captain, access, request, goal proposal) AND the branch's first word is a verb the client knows (web asks.ts:46-91, a hard-coded switch). Anything else falls to POST /api/asks/:id/decide, which records your words and "decides nothing else: a target keeps its own verb" (core asks.ts:310-339). Nobody tells the author. So three ways to ship a dead button: no target (Pix's first card), a target kind with no verb (this cap card: a goal setting), or a label the switch doesn't parse. The server files all three without a word and you find out by clicking.

So yes, hooks, in two parts. 1) A branch declares its act: a named verb on its target ("goal.setExploreCap", "captain.accept") or an endpoint, resolved and executed server-side on decide, not in the client switch. 2) The door refuses a click ask whose branches can't act: a click ask is by definition "press this", so a dead button is missing structure, same as a missing recommendation. Then an author either wires it or files it as a do ask, honestly.

This is the Workshop's code. I'd queue it directed to Pix, two steps: a short findings doc on every live card type and where its buttons die, then the PR. Say "queue it" and I'll do it. For this card: no button can set the cap today, so it's the goal tree, Onboarding goal, Exploration settings, 0.1, Save, or say "leave uncapped".
- **Mitchell:** sure
- **Secretary:** Queued: the button-hooks work is directed to the Workshop queue (as_zzvnadow9a), two steps: findings on where each card type's buttons die, then the PR with declared acts executed server-side and the door refusing a click ask with dead buttons.

Separate thing on your screen now: Pix re-proposed the Secretary runs grant with your shape, same 250k, three steps. I read "sure" as the queue, not the money. If you want it funded, say "fund it" and I'll press it as you.
- **Mitchell:** funded that, what do we do with this card for now
- **Secretary:** Two honest options. A) Do it by hand now: goal tree in the Town Hall, Onboarding goal, Exploration and money settings, type 0.1, Save. Then press "Set the cap" on the card so it closes with the truth. About 30 seconds. B) I defer the card behind the Workshop's hooks work, so it comes back when its button can actually set the cap, and Onboarding exploration stays limited only by the town cap until then. I recommend A: you already decided the number on Thursday, and B leaves the loop uncapped for days. Say "defer it" if you want B.
- **Mitchell:** ok where's the button? in the goals UI?
- **Secretary:** Yes, the goal tree. It opens as a sheet over the map: from the Town Hall, or from any building's Goals tab via "Goal tree at the Town Hall →", or by clicking the Onboarding goal's text anywhere. On the Onboarding goal there is a folded line "Exploration and money settings" that reads "no cap · exploration on" today. Open it. The first row is "Exploration cap" with a field in millions per day and a Save button (GoalTreePanel.tsx:314-321). Type 0.1 and press Save. The line then reads "cap 100k / day" and shows what it used today. Then press "Set the cap" on the card to close it.
- **Secretary:** Checked the queue. The cap card closed at 18:19 with "Set the cap", the captain card closed at 18:23 and the test account now captains the progressive disclosure goal, and you funded eight grants in a row. Two cards are left. Top: UI / UX asks 200k so the tool-call lines a stranger sees name their file or search term (today 56 percent name nothing). I recommend Fund: it is the weakest moment of the first minute and two small steps fix it. Below it: Pix's throwaway "Test card": that one is for the test account to press as part of the captains live check, not you. Leave it alone and Pix 1 decides it as the test account, then resets the account. Nothing else waits on you.

## Decisions

1. Ask card buttons must do the thing (Mitchell, 1:1 mt_m6qjva55rh 18:15: "buttons should just be connected to API endpoints that get hit when the user makes a decision. do we need to provide some kind of hooks affordance to ask card authors?"). Two steps, Workshop code. Step 1: a short findings doc: every live ask card type and target kind, which branches act today (web asks.ts:46-91 switch: grant, retainer, captain, access, request, goalProposal) and which fall through to POST /api/asks/:id/decide and record words only (core asks.ts:310-339); the three ways a dead button ships (no target, a target kind with no verb such as a goal's exploration cap, a label the switch does not parse), with the recent cases ak_3l51us2os7, ak_pmt8fn27fj, ak_52xdmgycz5. Step 2: the PR: (a) a branch declares its act, a named verb on its target or an endpoint, resolved and executed server-side at decide, with the client switch reduced to rendering; add the acts the recent cards needed (set a goal's exploration cap, accept a captain request); (b) the door refuses a click ask whose branches cannot act, as missing structure, with a message that names the act or says to file it as a do ask. Tell the Secretary and the managers when live. → Town Workshop queue (a fork of Pix)

## Closing

Quiet for 20 minutes; closed by the town.
