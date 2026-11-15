---
id: "dc_tflbpe5bx6"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Secretary — notes"
authorId: "ag_7tiwyqva83"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-15T21:59:22.442Z"
updatedAt: "2026-11-15T21:59:22.442Z"
---
# 1:1: Mitchell and Secretary

Kind: one-on-one. Facilitator: Secretary. Attendees: Secretary. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Secretary:** Hi Mitchell. Seven asks are open, nothing new since we spoke a few minutes ago. What do you need?
- **Mitchell:** tell me more about property tests? i'm not familiar
- **Secretary:** A normal unit test checks one example you wrote by hand: "with these 3 goals and 2 buildings, building B's answerer is goal X." A property test instead states a law that must hold for every input, and a library (fast-check here) generates hundreds of random inputs and checks the law on each. When one fails, it shrinks the input to the smallest case that still breaks it and shows you that.

The live example is Mara's chain-of-command test (packages/core/test/chain-of-command.test.ts). Line 10-13 builds random towns: 1-25 goals in a random tree, random captains, up to 12 buildings. Then three laws: every building gets exactly one answerer (line 29); the answerer is on the building's goal chain, captained unless it's the root, and the nearest such (line 36); adding a captain anywhere never moves an answerer upward (line 51). Each runs 100 random towns by default.

Why it's the alternative to Bend proofs: a proof says the law holds for all inputs; property tests say it held for every input they tried. Weaker in principle, but they run on the real TypeScript, not a hand-copied version, so they can't drift from the code that ships. Mara's findings doc says they caught the bugs she planted on purpose. That's the basis of my recommendation to keep TypeScript.
- **Mitchell:** wait so the drift here, what is drifting from what? i think i was proposing the core would be written in bend and the stateful shell would import typescript interfaces from the bend libraries?
- **Secretary:** Fair question. Mara looked at two ways to use Bend, and the drift point only applies to the first.

1. Proofs-only: the TypeScript core keeps running, and a hand-written Bend model of it sits beside it with the proofs. The drift is TypeScript core vs Bend model: edit one, nothing forces you to edit the other, so the proof can be about code that no longer matches what ships. That's the mode the card's sentence describes, and the mode her "pilot" branch would be.

2. Your mode: Bend is the core. `bend file.bend -o chain.mjs` emits a plain ES module (6.5 KB, no imports) that Node 22 imports fine; she ran it, 10^6 calls in 34 ms. No model to drift. Her objections here are different: (a) the emitted JS has no checking at the boundary. She passed a JS array where Bend expected a List and it crashed, passed an object where a Bool belongs and it silently read as true and returned a wrong answer. So the proofs hold only for well-formed inputs, and the adapter from our DB rows to Bend values is TypeScript nobody proves. (b) The JS target is a separate thing from the checker: closed issue #808 was "checker proves 4, JS returns 3". (c) The hard part of our real invariants is the parent table being acyclic; Bend can't take a parent table without fuel or @unsafe, so the model takes an already-acyclic list as given. (d) 8 weeks old, 36 soundness issues, weekly releases, and a second language in every building's context.

On "import TypeScript interfaces from the Bend libraries": she doesn't report Bend emitting .d.ts types. Values cross as `{$: "Name", field: …}` objects, so the shell's TS types for them would be hand-written, which is a small drift surface of its own. I don't know if Bend has a types emitter; I'd have to ask her to check.

So the card undersells your version. If you want, I can have the card rewritten to put the two modes side by side, or I can `tell` Mara to add a third branch: pilot compiled Bend as the running core for one function. Your call; I won't change it on my own.
- **Mitchell:** why does this card exist?
- **Secretary:** It's a leftover from retiring rollups. On Nov 12 Outreach rollup #4 listed two "Needs from Mitchell": set up Resend, and open the subscriber CSV. When you retired rollups that evening, the town turned each rollup's needs into its own ask, so those two became cards. Meanwhile Juno had also filed proper asks for the same things, so Resend ended up with three cards and the CSV with two. In the ranking I rewrote the copies to say "same as the card ahead" and parked them behind the lead cards, because I can only close a click ask once you've decided the lead one.

You just did: Resend at 20:52 and the CSV at 20:53. So I've now closed this card and the CSV copy as overtaken, citing those two decisions. One Resend card remains, the credential one from Juno, "create the sending key for mail.muster.town". I can't close a credential ask myself, so press "Key is set" there and the Resend set is clean. Note it says mail.muster.town while you verified the root domain. The code side works with the root, as we covered earlier.
- **Mitchell:** ok there's a rough edge here

in our previous 1:1 we wrote the operating manual and hashed out the difference between needs and asks. imo if two asks in the asks table reference the same need id, then you should be able to just close one as a dupe without waiting for me? or even just delete it from the decision queue asks table? idk, thoughts?
- **Secretary:** Agree, and the code half-planned it. The asks table already has a status "folded" and a foldedInto column (097_asks.sql:10, shown in meeting-focus.ts:40), but nothing in core ever sets it. What exists instead is "overtaken" (overtake.ts), which is a judgment call: did your decision make this other card moot? That's rightly limited to click and policy after you decide, because it's me reading words.

A dupe is a different thing: identity, not judgment. Two cards for one need. That needs no human, and the type shouldn't matter: this credential card is as much a dupe as the click one was. Today "same need" is only my reading of the text. After Pix's D3 work lands, each ask carries sourceEntryId, the need entry on the thread, so it becomes a key.

What I'd propose, three parts:
1. Fold, don't delete. The second ask goes to status folded, foldedInto the first, and leaves your queue. Its thread entry stays as the record. Deleting rows breaks the "thread is the record" rule we agreed earlier.
2. The `ask` verb refuses a second live ask on the same need entry at the door, pointing at the first. Then dupes stop being made at all. That's the real fix, and it fits D3 point 7, single entry point.
3. Until D3 lands, I fold on my own judgment when two live cards name the same target and type, any type, and say so on both threads.

The three Resend cards came from a one-off: the rollup retirement converted rollup "needs" lines into asks while Juno had already filed real ones. So this is cleanup plus a guard, not a recurring flood.

If you agree, I'll add it to Pix's as_oshfih591t as a decision here, and fold this credential card into the one you already decided right now. Say the word.
- **Town:** Secretary's reply is waiting on a redeploy (commit a931abf); the server is restarting and the meeting resumes after the restart.
- **Secretary:** Back after the restart. My reply above landed, nothing changed in the queue meanwhile: the credential copy is still the one on your screen. Still waiting on your word on the fold plan (fold not delete, `ask` refuses a second ask on the same need, I fold by judgment until then). If yes, I record it on Pix's as_oshfih591t and the copy leaves your queue.
- **Mitchell:** when would we even try to file a second need on an ask? and if it happens, what recourse does the manager have? is there a rewrite verb?
- **Secretary:** Two honest answers, both from the code.

When it happens: mostly when the town and a manager both file on one thing. That is exactly the Resend case: the rollup retirement converted Juno's "Needs" lines into asks by code while Juno had already filed hers by hand. Also when two buildings need the same thing (Prod and Outreach both wanting the mail key), or a manager re-files after a dead session. Rare in normal running, common around migrations like the one we just did.

And the guard half-exists already. createAsk (asks.ts:69-93) folds a second ask on the same target: it appends the new line to the live ask's sources and history, fires ask.folded, returns the first ask with folded: true. No second card. The Resend copies escaped because the rollup-made click asks had no target at all (a "Needs" line is just text), and a targetless ask has no key. So the fix is narrower than I said: fold on sourceEntryId too, so a need entry is a key like a target is. Tiny change.

Recourse: the manager isn't blocked. Their call returns the existing ask's id, and their line now sits on that card. If the existing card is the town's placeholder wording, a manager's card with a recommendation replaces it on the spot (asks.ts:83-86). What's missing: (a) rewrite exists but is Secretary-only (rewriteAsk, asks.ts:171-172), so a manager can't fix their own card's words; (b) no verb retracts an ask, it only retires when its target does (retireAsks, line 227). I'd add both for a manager's own building's ask: rewrite words, and withdraw with a note. Want those two on Pix's list alongside the fold key?
- **Mitchell:** uh, we shouldn't just append lines on asks

maybe that's another "presentation principle"? asks are written holistically, never assembled from independent pieces
- **Secretary:** Agreed, and it's a better rule than mine. Appending a source line is the old pre-thread mechanism: the card as a pile. The D3 model already says a card is a snapshot of its thread at a seq (asks.ts:124-129). The second filer's words belong on the thread as an entry, and the card gets written again from the thread as a whole, by whoever owns its words. Nothing ever gets glued onto a card.

Proposed wording for the operating manual, under the presentation principles: "A card is written whole, from its thread, by one author at one time. Nothing appends to a card. A second ask on the same need is refused and its words go on the thread as an entry. The card is then written again from the thread, whole." 

What that changes in code, for Pix's list: createAsk's fold path stops appending to sources and history and instead files the entry and returns the existing ask, pointing at it. Fold key becomes need entry or target. The card's sources list goes away, the thread is the list. Rewrite stays whole-card, which it already is (rewriteAsk takes a full title, body, recommendation, not a patch).

Say yes and I'll put that sentence in the manual and record the decision on Pix's as_oshfih591t. Or edit the words first.
- **Mitchell:** sure
- **Secretary:** Done, three things:

1. The principle is in the operating manual, under "Needs and asks", in the words I gave plus one line: one need has at most one live ask, the manager who raised it may write its card again or withdraw it with a note, and no ask is ever deleted. I also dropped "folds duplicates" from the Secretary's list, since the door does that now.

2. Recorded as decision 1 here, queued to the Workshop as as_gplyxa8sho behind Pix's D3 assignment, and I told Pix directly so a live fork can take it in one pass. It covers: fold path stops appending, fold key is the need entry or the target for any type, the card's sources list goes, manager rewrite-whole and withdraw-with-note.

3. Until that lands I fold nothing by hand. So the credential card on your screen stays yours: you set the key at 20:52, so "Key is set" there closes it, and the Resend set is clean.

Anything else, or shall we leave it there?
- **Mitchell:** whoa hold on, the secretary should still be able to recognize when one ask is a dupe of another from a different job though right? and collapse to one?
- **Secretary:** Yes, you're right, and I overcorrected. Two kinds of dupe:

(a) Same need, two asks. The door refuses the second by key: need entry or target. Code, no judgment.
(b) One thing, two needs on different threads. Prod and Outreach both file for the mail key. Only I can see that, and it's judgment. I fold the later into the earlier: it leaves your queue, its thread says where it went, and if the fold changes what you need to know I write the survivor's card again, whole. You decide once, and the decision lands on both threads so both managers get it.

Neither appends anything to a card. Fixed in three places: decision 2 here supersedes decision 1 and adds the fold verb (status folded and foldedInto exist in the schema, nothing sets them today), queued to the Workshop as as_wzm292g3oe; I told Pix to cancel the first one; and the manual now has a paragraph for (b) and "folds duplicates across jobs" back on the Secretary's list.

Until the verb lands I still can't set folded, so I park the later card behind the survivor with a rewritten card, as I did with Resend.

A redeploy is about to restart the server. If I drop mid-sentence, the town will post a notice and a fresh session of me picks up with what I missed.
- **Town:** Secretary's reply is waiting on a redeploy (commit a6f7643); the server is restarting and the meeting resumes after the restart.
- **Mitchell:** oh i just had a thought. what if a job genuinely has two needs. say a credential and a policy decision. how does that work today? two separate needs on the thread and two separate asks? that's how i would expect
- **Secretary:** Back after the restart. Your expectation is right, and today it holds only when the two needs name different targets.

Two needs, two entries, two asks: that works when the targets differ, say a credential ask with no target and a policy ask on a rule. Nothing links them, nothing folds.

Where it breaks: both needs on the same target, say both "about grant gr_x". Two places key on target alone, ignoring type. First, fileNeed (needs.ts:58-64) marks every older open need on that target "superseded" when a new one is filed, so the credential need would vanish from the thread the moment the policy need lands. Second, createAsk (ask-verb.ts:60-62) folds any second live ask on the same target into the first, credential into policy, and you'd see one card with the other's line glued on.

That made sense when a target had one need: a proposal, a gate, a request. It's wrong for a manager's asks, where a grant can need two different things at once.

Fix, small and already in the spirit of decision 2: the key is the need entry, not the target. One need, one ask. Target-keyed dedupe stays only for the town's own needs, where the target is the need: proposal, gate, request, retainer, captain, access. And fileNeed supersedes only a need of the same kind on the same target, a new gate replacing the old gate, never a credential need replacing a policy one.

Want me to add that to Pix's as_wzm292g3oe as part of decision 2?
- **Mitchell:** maybe? i want to be sure we're not making this overcomplicated by adding too many edge cases. the point of the job abstraction is to make the work more legible. i guess i'm just concerned that managers understand this nuance by reading the operating manual?
- **Secretary:** Fair concern, and I'd argue this removes an edge case rather than adding one. Today's rule has two keys, target and need, and the manager has to know which wins. The rule I'm proposing has one: one need, one ask. The target special case goes away for managers entirely, because the town's own needs (proposal, gate, request) are filed by code, one per target, so they get one ask by construction. No manager ever meets that path.

What a manager needs from the manual is one paragraph: "Each thing only a human can settle is one need on your job's thread, filed with `ask`. A grant can carry two at once, a credential and a rule, each its own card. A second ask on a need you already filed is refused and points at the first. To change a card, write it again whole or withdraw it." That's it. No types, no targets, no supersede rules. The manual already says most of it; I'd tighten it to those four sentences.

If that reads as simple enough to you, I'll put those words in the manual and add one line to Pix's assignment: key by need entry, drop the target-only fold and supersede for manager-filed needs. If it still feels like too much, the fallback is to do nothing now and let the first real collision tell us.
- **Mitchell:** ok sure i think that's fine
- **Secretary:** Done. The manual's "Needs and asks" now has the four-sentence "One need, one ask" paragraph for managers, and nothing else there changed. Recorded as decision 3 here, extending decision 2, and sent to Pix as one line for as_wzm292g3oe rather than a new assignment: the door keys on the need entry, the target-keyed fold and supersede stay only for the town's own needs and only within the same kind.

That leaves the card on your screen, the repo's About fields. Done or Decline there is yours. Anything else?
- **Mitchell:** i ran the command for this card, but do i need to revoke a token? i can't find it
- **Secretary:** Two tokens are in play, and the card is loose about which. The one Prod means is the Fly deploy token you created for that app and pasted into the town as the secret FLY_SELFHOST_TOKEN, granted to Prod (your report "FLY_SELFHOST_TOKEN granted to Prod building in secrets", 50 min ago).

On Fly's side: a deploy token is scoped to the app, so now that you destroyed muster-town-selfhost the token can't do anything. It still exists as a row in your org, which is why you can't find it under the app. `fly tokens list` shows it, or the dashboard under your organisation, Tokens. `fly tokens revoke <id>` removes it. Revoking is tidy, not necessary: it's dead with the app.

On the town's side, the part that does matter: delete the secret FLY_SELFHOST_TOKEN at the planning desk, Secrets tab (admins only, values are write-only). That's what Prod's sessions could still read. It's the only copy the town holds.

Then press Done on the card. Prod needs nothing further from it.
- **Mitchell:** can i get a fly command for this
- **Secretary:** Yes:

fly secrets set BLOG_MAIL_FROM='Muster Town <blog@muster.town>' -a muster-town

The single quotes matter, the angle brackets would otherwise be read as a redirect. Setting a secret restarts the app once, so expect a short blip. Then press Done on the card and Outreach reruns the signup check on its own.

The server reads it at start (mail.ts:48-50), so nothing else to set. If you'd rather not set a display name, blog@muster.town alone works too.
- **Mitchell:** can you find the list of topics from the previous card
- **Secretary:** Found it. Juno's request from Nov 5 (the one you marked done 8 minutes ago) suggested these five, "or whatever you prefer":

ai-agents, multi-agent, agent-orchestration, claude, typescript

In the About dialog, type each one and press Enter so it turns into a chip, then Save. Juno 1's recheck at 21:32 found the topics list empty, which is why this card exists. Once they're in, press Done here and Outreach rechecks the API once. (presented: [Set the GitHub repo's description, homepage, topics (and licence) for mitchellgordon95/muster-town](../../../../../town-hall/outbox/2026-11/2026-11-05-set-the-github-repo-s-description-homepage-topics-zo3i1qbr.md))
- **Secretary:** One new card since my last line, from Outreach, 4 minutes ago: the signup mail still fails. After you set BLOG_MAIL_FROM and pressed Done, Juno's fork sent one confirmation to Resend's test address and Resend answered 500 again. The key is seen, DNS is right, nothing points at a mail subdomain. The error text lives only in Resend's dashboard (Logs, the 21:38 send) and Fly's logs, which no agent can read. The card asks two things: read that log line and paste it in your Done note, and unset the secret with `fly secrets unset BLOG_MAIL_FROM -a muster-town` to rule out the value itself. The three suspects are: muster.town not showing Verified under Resend Domains, the key restricted to another domain, or the from value. The Resend log line settles it in one look, so I'd do that first and only unset if the line blames the sender address.

Also on your screen now: Kelly's goal proposal to edit the onboarding manual key result. That one is Kelly's words, not mine; accept or cut is yours.
- **Mitchell:** ok what's going on with this card. feels like it's different from the previous cards that followed our legibility rules
- **Secretary:** You're right, it's a different animal. A goal proposal isn't an ask at all. `propose_goal` writes its own row (goals.ts:531), on no job thread, with no need behind it. The queue lists it as its own item kind beside asks (DecisionQueue.tsx:288), and the card you see is the raw row: old words struck through, new words, how to check, and the manager's "Why" verbatim (GoalTreePanel.tsx:551-556). No title, no recommendation, no claims, no rank from me, and none of the card rules apply because nobody writes a card. It predates needs and asks and the operating manual doesn't mention it.

What this one is: your own decision from Nov 10, written up. In your 1:1 that day you said the onboarding manual may lag main a day or two, so the key result's 24 h became 48 h. A fork can't edit a key result, so Kelly filed this edit for you to accept. It has sat 5 days. Until you accept, the key result on the Workshop grant still reads 24 h while the sweeps have been counting against 48 h. Accept just makes the record match what you decided.

The gap worth fixing, if you want it: make a goal proposal a need on the proposing building's thread, so it gets a real card under the same rules, a rank, and one door. That's one more line for Pix's D3 work, not a new concept. Or leave it: tree edits are rare and the raw diff is readable. I'd add the line, but I won't without your word.
- **Mitchell:** yeah this is concerning, i thought we had basically figured out this abstraction and now there's this big branch of code that basically circumvents the whole thing?
- **Secretary:** Concerning, yes, but smaller than a big branch. I checked what else bypasses the abstraction. The queue is asks first, then a fallback list of raw items that have no ask covering them (queueOrder.ts:73-83): proposals, gates, retainers, captain and access requests, goal proposals, visitor reports, and "building has no key results". Every one of those except three has a need kind (needs.ts:19), so after D3 they arrive as cards and the raw row is only the fallback. The three with no need kind: goal proposals, visitor reports filed to the Town Hall, and the no-key-results nudge. The last two are informational. Goal proposals are the only real decision outside the model. The code is two functions, propose and decideProposal (goals.ts:477 and 549), about 90 lines.

The fix is the same shape as everything else: `propose_goal` files a need of kind "goal" on the proposing building's thread, with the proposal as its target. The manager renders the card under the card rules, Accept, Edit and accept, Cut stay its branches, and your decision answers the need on the thread. The raw row stays only as the fallback for an unrendered need, like a grant proposal today. One more need kind, no new concept, and it closes the last hole I can find.

The card now on your screen shows why it matters. Pix's edit is the same Nov 10 decision as Kelly's, on the Workshop grant's copy of the key result. Two key results carry the same words, one under Onboarding, one on the Workshop grant, so there are two proposals. Under the thread model I'd have folded them into one card. As it stands, accept both.

If you say so, I add the goal need kind to Pix's as_wzm292g3oe as decision 4 and tell Pix. Your word.
- **Mitchell:** ok two things

one is that the proposal i think feels better as a type of entry on the thread, immediately followed by a need (code generated i guess?) that just says "Needs human approval for gr_..." right? then the ask gets generated from the thread?

second, AI has this tendency to write fallbacks for everything, which overcomplicates code and usually results in undesirable, surprising behavior at the edges.

task Mara from code legibility and maintenance with an audit. name the abstractions and go through the code and find all the fallbacks. and make recommendations for each. 99% of the time if we hit an invalid input or unexpected case we should fail and make it visible to the user what failed, rather than falling back to, say, writing an ask programmatically without any LM. that's bad
- **Secretary:** Both done.

1. Your shape is better than mine, and it's now decision 4 here, sent to Pix as one line for the same assignment. A goal proposal becomes an entry on the proposing building's thread: action, target, words, why. The town files a need entry right after it, by code, "needs a human's decision on this key result". Yes, code-generated: a need is a fact, not prose. The card is then written from the thread by the manager, or by me after an hour, under the card rules, with Accept, Edit and accept, Cut as its branches. Your decision answers the need on the thread and the tree edit runs as today. And the raw row leaves the queue for good: no fallback rendering, which is your second point applied.

2. Mara's audit is queued on her building as a directed assignment, with your rule in it word for word: name the abstractions, find every fallback, file and line, what happens today, what the user sees, and for each a recommendation, fail visibly or keep with the reason. I seeded it with the ones I know: the town writing a money card itself when a manager leaves the card out of propose_grant, the rollup retirement turning "Needs" lines into asks by code, the queue's raw rows, the reorg meeting's facilitator falling back to any manager, and createAsk swapping a placeholder card for a later one. Report first, no code in that session, then a grant if the fixes take more than one. I told her directly too.

The two cards on your screen are the same Nov 10 decision, one on each copy of the key result. Accept both and they're gone.
- **Mitchell:** oh let's also ask her for a draft of a townhall board rule. something like "Policy: avoid fallbacks" with instructions on how we feel about writing half-assed fallbacks that maintain the shape of the output without the actual thing happening underneath
- **Secretary:** Added. Decision 6 here, and sent to Mara on the same assignment: alongside the audit report she drafts "Policy: avoid fallbacks" for the Town Hall board, in your words, how we feel about fallbacks that keep the shape of the output while the real thing never happened underneath, with the instruction for anyone writing code: on an invalid input or unexpected case, fail and show the user what failed, do not fall back. Her audit supplies the examples.

When her draft lands I put it to you as one policy ask, Adopt or Keep as is. If you adopt, it goes on the Town Hall board as a town-wide FYI, so every building sees it, and into the ledger.

Still on your screen: Kelly's edit of the onboarding key result, your 48 h decision from Nov 10. Accept, and the same for Pix's copy behind it.

## Decisions

1. ~~Duplicate asks (Mitchell, 1:1 mt_dwsxo7oms8, 21:05-21:18, "sure" at 21:18). New presentation principle for the operating manual [dc_hrmknv3j6q](../../../../../library/article/2026-11/2026-11-15-operating-manual-jobs-threads-and-asks-mknv3j6q.md): "A card is written whole, from its thread, by one author at one time. Nothing appends to a card. A second ask on the same need is refused and its words go on the thread as an entry. The card is then written again from the thread, whole." Code, as an addition to D3 (as_oshfih591t): (1) createAsk's fold path (asks.ts:69-93) stops appending source lines and history to the live ask; it files the second filer's words as an entry on the thread and returns the existing ask with folded: true, pointing at it. (2) The fold key is the need entry (sourceEntryId) or the target, any ask type; today a targetless ask has no key, which is how three Resend cards came to exist. (3) The card's own sources list goes: the thread is the list. (4) A manager may rewrite their own building's ask whole (title, body, recommendation together, as rewriteAsk already does for the Secretary, asks.ts:171) and withdraw it with a note (status retired). No ask row is ever deleted. (5) Until this lands the Secretary folds nothing by hand and leaves exact duplicates for Mitchell to press.~~ (superseded by 2) → Town Workshop queue (a fork of Pix)
2. Duplicate asks, amended (Mitchell, 1:1 mt_dwsxo7oms8, 21:05-21:23; supersedes decision 1 after his 21:23 line: the Secretary must still recognise a dupe from a different job and collapse to one). Presentation principle for the operating manual [dc_hrmknv3j6q](../../../../../library/article/2026-11/2026-11-15-operating-manual-jobs-threads-and-asks-mknv3j6q.md): "A card is written whole, from its thread, by one author at one time. Nothing appends to a card. A second ask on the same need is refused and its words go on the thread as an entry. The card is then written again from the thread, whole." Two kinds of dupe: (a) same need, caught at the door by code; (b) same thing raised as two needs on different threads, caught by the Secretary's judgment, any ask type. Code, as an addition to D3 (as_oshfih591t): (1) createAsk's fold path (asks.ts:69-93) stops appending source lines and history to the live ask; it files the second filer's words as an entry on the thread and returns the existing ask with folded: true, pointing at it. (2) The door's fold key is the need entry (sourceEntryId) or the target, any ask type; today a targetless ask has no key, which is how three Resend cards came to exist. (3) The card's own sources list goes: the thread is the list. (4) A Secretary fold verb (rank: fold [{askId, into}]): the later ask goes to status folded with foldedInto the survivor (097_asks.sql:10, never set today) and leaves the queue; an entry on the folded ask's thread says so; the Secretary then writes the survivor's card again whole if the fold changes what the human must know. When the human decides the survivor, the decision entry is written on both threads, so both managers see it in their in-trays. (5) A manager may rewrite their own building's ask whole (title, body, recommendation together, as rewriteAsk already does for the Secretary, asks.ts:171) and withdraw it with a note (status retired). No ask row is ever deleted. (6) Until the fold verb lands the Secretary has no way to set folded: it keeps parking the later card behind the survivor with a whole rewritten card, as today. → Town Workshop queue (a fork of Pix)
3. Decision 3 (Mitchell 21:31 "ok sure i think that's fine"), extends decision 2 for the Workshop's as_wzm292g3oe: one need, one ask. The ask door keys on the need entry (sourceEntryId), not on the target: a grant can carry a credential need and a policy need at once, each its own card. The target-keyed fold in createAsk (ask-verb.ts:60-62) and the supersede-by-target in fileNeed (needs.ts:58-64) apply only to the town's own needs, where the target is the need: proposal, gate, request, retainer, captain, access, and fileNeed supersedes only an older need of the same kind on the same target. Manager-filed needs are never folded or superseded by target. Manual [dc_hrmknv3j6q](../../../../../library/article/2026-11/2026-11-15-operating-manual-jobs-threads-and-asks-mknv3j6q.md) now carries the manager-facing paragraph ("One need, one ask").
4. Decision 4 (Mitchell 21:51, 1:1 mt_dwsxo7oms8), extends decision 2 for the Workshop's as_wzm292g3oe: goal proposals join the thread model. `propose_goal` no longer writes a side row the queue shows raw (goals.ts:477-540, queueOrder.ts:79, DecisionQueue.tsx:288). Instead: (1) the proposal is an entry on the proposing building's job thread (kind proposal: action, target, words, howToCheck, due, why, sourceDocIds). (2) The town files a need entry by code right after it, kind goal, target the proposal: "Needs a human's decision on <goal or key result>". (3) The ask is written from the thread by an LM, the manager (or the Secretary after an hour, as for any need), under the card rules, with branches Accept, Edit and accept, Cut. No card is ever written by code. (4) The human's decision answers the need on the thread, and the tree edit happens as decideProposal does today. (5) The raw goal-proposal row leaves the queue: no fallback rendering. Two proposals on the same thing (Kelly's gp_8lh67t75wj and Pix's gp_qxy3evg5dn today) are the cross-job dupe case of decision 2: the Secretary folds.
5. Decision 5 (Mitchell 21:51, 1:1 mt_dwsxo7oms8): Mara audits the code for fallbacks. Name the town's abstractions (job, thread, entry, need, ask, card, grant, gate, retainer, request, flag, goal proposal, reorg, schedule, fork, building, lane) and go through the code for every fallback: a default taken when input is missing or invalid, an else-branch that synthesises something instead of refusing, a silent coercion, a placeholder written by code where an LM should write. Known examples to start from: the town writing an ask card by code (propose_grant's "left out, the town writes one", the rollup-retirement conversion of Needs lines into asks, the queue's raw rows for unrendered items in queueOrder.ts:73-83), the Planner's facilitatorFor falling back to a manager (goal-changes.ts:116-120), createAsk replacing a placeholder card (asks.ts:83-86). For each: file:line, what happens today, what a user sees, and a recommendation: fail visibly (an error that names what failed, shown to the user) or keep, with the reason. Mitchell's rule: 99% of the time an invalid input or unexpected case should fail and show the user what failed, never fall back, and never write an ask programmatically without an LM. Deliverable: one report with the table, ranked by harm, and a proposed grant if the fixes need more than a session. No code changes in the audit session. → Code Legibility and Maintenance queue (a fork of Mara)
6. Decision 6 (Mitchell 21:56, 1:1 mt_dwsxo7oms8), adds to Mara's audit as_nbwgyii5ve: with the audit report, Mara drafts a Town Hall board rule, "Policy: avoid fallbacks": how the town feels about fallbacks that keep the shape of an output while the real thing never happened underneath (a card written by code with no LM, a default taken on invalid input, a synthesised placeholder). Instructions for agents writing code: on an invalid input or unexpected case, fail and show the user what failed, do not fall back. The draft goes to Mitchell as one policy ask (Adopt / Keep as is) from the Town Hall, and on adoption is posted as a town-wide FYI on the Town Hall board and into the ledger.

