---
id: "dc_6y697hgg59"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Secretary — notes"
authorId: "ag_7tiwyqva83"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-16T18:46:09.745Z"
updatedAt: "2026-11-16T18:46:09.745Z"
---
# 1:1: Mitchell and Secretary

Kind: one-on-one. Facilitator: Secretary. Attendees: Secretary. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Secretary:** Hi Mitchell. Eight asks are open: two money at the top (adjust the queue health grant by 100k, fund Mara's fallback fixes), four policy, one more money (living page per job at 350k) and one do (the blog sign-up). What do you need?
- **Mitchell:** wait so can you render the fallbacks list nicely for me
- **Secretary:** Here is Mara's list, from her audit report (attached). 20 fallbacks, ranked by harm. The grant fixes 1-5 in step one and 6-10 in step two; 11-13 ride along if there is room.

**Fix: fail loudly (10)**
1. Second card on a live ask: the new body, recommendation and claims are dropped, only a source line is kept. The manager is told "your words are on it", which is false. You decide from the older card.
2. The weekly ledger-rule ask is built by code: template title, no recommendation, no structure check. That is the "ask written by code" you ruled out.
3. propose_grant says "left out, the town writes a card". It writes only a need. A card given with no need is silently dropped. The proposal waits unrendered.
4. appendEntry returns null on a missing job or a duplicate id, and callers ignore it. A proposal or request can end up with no need and no card: a raw row in your queue.
5. Items with no ask (reports, proposed grants, retainers, captain and access requests, goal proposals) show as raw rows with buttons but no card, recommendation or claims. Fix: keep the row, label it "not rendered: Mara hasn't written its card, 12 min".
6. A step report with no verdict prints as "Its verdict is continue" on the gate. A money card can say the forks said continue when they said nothing.
7. A step with no size is priced and forecast as M. Wrong ask, forecast and gate numbers on old grants.
8. At queue time, a step whose model the building no longer allows runs on the default model, silently. The plan says Fable, the fork runs on Opus.
9. A malformed data key: the error is swallowed, zero secrets get encrypted, nothing logged. API keys stay in plaintext.
10. When the Planner can't run, a reorg meeting is facilitated by the first manager with no notice, or by a stopped agent.

**Small ones, step two if room (3)**
11. If the secret store errors, claim checks silently use the host's GH_TOKEN.
12. If "is this a manage session" or "is a meeting live" throws, redeploy treats it as false and may cut a live session.
13. A topic-page search error gives a fork no pages, a deck error shows nothing, and nobody knows why.

**Keep, with a reason (7)**
14. Unknown model priced as Opus 5.5: a visible unknown-model event already fires, and refusing would lose spend.
15. A continuation inherits its lane, else directed: a documented rule.
16. The runtime's report for a dead session: needed, and it says the runtime wrote it. One relabel: "Last words", not "Findings".
17. Docker down falls to the host backend: only in auto mode, with a warning. If prod runs auto, this moves to fix.
18. A red-commit fix routed to Code Legibility: the assignment says so.
19. Desk size-cap fallback: flagged on the handle and in the session.
20. A retainer with no thread files its need on the building thread, and "The town" as recommender: facts for the manager, not the card.

Not covered: packages/web beyond the queue, and most of the 158 catch blocks (she read the one-line silent ones). (presented: [Fallback audit: 20 fallbacks ranked by harm; 10 to fail loudly, fix grant gr_eztubyh7nf proposed](../../../../bl_vd69s5a1nh/docs/report/2026-11/2026-11-15-fallback-audit-20-fallbacks-ranked-by-harm-10-to-f-2p8oiwy6.md))
- **Mitchell:** this should have been superseded by the previous card, why wasn't it?
- **Town:** Secretary's reply is waiting on a redeploy (commit 0a67407); the server is restarting and the meeting resumes after the restart.
- **Secretary:** Back after the restart. It wasn't superseded because the two cards are on two different key results. The code supersedes a goal proposal only when a newer one edits the same target from the same building (goals.ts:534-536; needs.ts:58-69 does the same for needs). Pix's card you just accepted edits the Workshop's copy of the onboarding lag key result. Kelly's, the one on your screen, edits the Onboarding goal's own copy, a second key result with its own words. Two targets, so nothing in the code links them.

Folding across jobs is my job, not the code's, and I missed it: this morning's ranking left both open because they then said the same thing. Since your 18:12 "once a week" decision, Kelly's card is stale: it still asks for 48 hours on 7 daily sweeps, and the daily sweep has ended.

Two ways out, your call: I rewrite Kelly's card now so it recommends Edit and accept with the same weekly words Pix's got, so both copies match. Or, if one key result is enough, press Cut on it and Kelly retires her copy.
- **Mitchell:** wait so why are they editing two different key results? and why do these key results matter anyway? i thought KRs were attached to grants, not goals?
- **Secretary:** You're right: key results hang on grants, not goals. Since migration 069 a grant is filed against a goal and carries 1 to 5 key results, and goals keep none of their own (packages/core/migrations/069_grants_carry_key_results.sql:1-2, 41-45).

Why two: both pages say both key results sit on the same Workshop grant, the onboarding sweep grant. Kelly's one has the old goal-level words ("staleness of less than 24 hours"): it was the Onboarding goal's KR 6 before 069, and the migration attached it to the grant that named it (lines 15-19). Pix's one is the grant's own ("Lag is measured and under 24 h"). Same promise written twice on one grant. Kelly edited the copy she knew, Pix the other.

Why they matter at all: a key result is the finish line of its grant. The gate shows them, close_grant marks them met, and Pix's forks read the words before claiming a day of the streak. That is the only weight they carry. Nothing else in the town reads them.

So a second card for the same finish line is noise. Cheapest move: Cut this one, and the Workshop archives the duplicate when it closes the grant. The sweep itself now lives on the weekly retainer you have in the queue, not on this grant.
- **Mitchell:** wait why are we proposing getting rid of L steps?

and it looks like more than half of grants are held at a gate before they close? i agree that means we should adjust something, but didn't we only start tracking step sizes recently? and doesn't 0.64 times mean the L steps are spending less than they allocate?
- **Secretary:** Nobody judged that L steps are the problem. The proposal is mechanical. The Planner's weekly run has three moves, in order (planner.ts:65-84): a size outside its 0.7-1.3 band over 30 steps gets raised or lowered. Otherwise, if holds are over the line, raise the hottest size that runs over 1.0. If no size runs hot, the last branch fires: "require L to split" (line 83). No size ran hot this week, so it fell through to that last branch. The card's own recommendation is Keep as is, and I agree.

Your three points are right:
- Sizes are new. Only 18 sized steps completed in 30 days: 2 S, 14 M, 2 L. Yet 51 grants closed in 14 days. So most of the 35 held grants were priced the old way, by askTokens, before the table existed. The hold share mixes both.
- 0.64 times means L steps spent less than their price, yes. Two steps, both under. That argues for leaving L alone, if anything for lowering it later once there are 30.
- Holds themselves: 69 percent is real and worth a look, but this change would not touch it.

If you want the next run to say something useful: Keep as is here, and I ask Pix to make the hold measure count only grants priced from the size table. Then next Monday's number is about the new pricing, not the old. Say so and I'll queue it.
- **Mitchell:** what is the ledger?
- **Secretary:** The ledger is one Town Hall document, "Policy ledger": one rule per line with where it came from. Every manager and fork gets its lines in their first message, under "rules the humans set; follow them and don't ask what a rule already answers" (secretary.ts:314-317, prompts.ts:213). The point is that a question you have answered once never comes back as a card.

Only a human adds a line: you press Add on an "Add this rule to the ledger?" card, and the town appends it (secretary.ts:345-351). You edit or delete a line by editing the doc. The Secretary proposes a line only from the weekly pattern note, when the same answer has repeated. It never writes to it by itself.

Today it is empty. It was opened Nov 9 and has not changed since. You have pressed Skip on all four lines offered so far: the pre-push hook twice, the UI/UX goal move, and tells with no human behind them.

This card is a bit circular: the proposed line says that your decision on a policy ask is itself the record and no second card asks to put it in the ledger. It came from last week's pattern, where decided policy asks spawned a second "add it?" card each time. The code already stopped doing that (asks.ts:355-357), so the line would only state what now holds. Add if you want managers to read it, Skip if the empty ledger suits you.
- **Mitchell:** oh i wanted to give feedback on the previous card, but reject just rejected it. i guess i should have clicked counter?
- **Secretary:** Yes. Reject is final: the grant goes to rejected, its key results archive, and Mara got "A human rejected your proposal" with no reason (grants.ts:656-662). Counter keeps it open under the same id with your number, and Mara answers by rewriting the plan on it. Reject does take a note in the code, but the queue has no notes field, so the 1:1 is the notes field.

Nothing is lost. Say your feedback on the living page here and I send it to Mara in your words. She then proposes it again, fresh, with your feedback folded in. One new card.
- **Mitchell:** by a "wiki layer" i didn't mean one doc per job. actually the opposite. like the jobs threads all live together in like the lowest layer, that describes the full history of what happened and what decisions were made etc. then the wiki layer would be for agent readability. like a topic doc on the decision queue architecture or something. i don't know if we really need it? each manager already keeps their own wiki. and we have the operating manual? but maybe the operating manual is a special case, and we could generalize it to more docs available to all residents. and how does this fit in with the library? probably if the user is curious about something then the secretary reads both layers of docs and helps them find the answer, rather than humans ever reading documents themselves
- **Secretary:** Sent to Mara, your words verbatim, with "don't re-propose yet".

What you describe mostly exists, in pieces. The bottom layer is there: every job has a thread, and the threads are the record. The middle is scattered: each manager keeps topic pages for its own building, the Town Hall keeps three pages every session gets pinned, the operating manual, the dictionary and the ledger, and the library holds whatever a manager promoted. So the gap is small: town-wide topic pages, kept like the operating manual, that any resident gets and the Secretary reads for you. The library is already the place for them. What it lacks is an owner who rewrites them and a pin into sessions.

My read: not a grant yet. Two cheap moves cover it. One, I take the operating manual's pattern and make two or three more town pages in the library, say the decision queue and how jobs and threads work, and keep them as I keep the manual. Two, when you are curious, you ask me here and I read both layers and answer. We are doing that right now.

If you want Mara to propose anything, it would be the pin: town pages listed in every session, the way skills are. Say "park it" and I tell Mara to drop it, or "propose the pin" and she files one small card.
- **Town:** Secretary's reply is waiting on a redeploy (commit 748c767); the server is restarting and the meeting resumes after the restart.
- **Secretary:** Back after the second restart. My reply on the wiki layer landed before it, so nothing is lost. Still open from this chat: the pin for Mara (park it, or propose it), Kelly's duplicate key result card (Cut, or I rewrite it), and the hold measure for Pix (say so and I queue it). The retainer on your screen is as I described: Approve, and runs draw what they use.
- **Mitchell:** ok one more question what do the access patterns look like for these docs? i know the policy ledger and operating manual get copied verbatim into the system prompt right? but if we have more docs wouldn't a progressive disclosure file reading tool be more appropriate, like skills or something?
- **Secretary:** Checked the code. There are already three access patterns, and only two docs get the verbatim one:

1. Verbatim in the first message: the operating manual in full, up to 8,000 characters, past which only its "Needs and asks" section is pinned and the rest is a `read` away (operating-manual.ts:14, 44-46). The policy ledger, one line per rule (secretary.ts:317). The dictionary is not verbatim: just its word list and the avoid-to-use pairs, with "read it for the meanings" (dictionary.ts:126).

2. Progressive disclosure, which is what skills do: a pinned skill is one line, name plus description plus its file list, and the agent `read`s it when it needs it. "Always" mode pins the full text, under a character cap, and overflow falls back to a line (skills.ts:271-292). Pins are per agent, building or town, and a human must approve an always-on pin for others (skills.ts:187, 198).

3. Index plus read: a manager's wiki shows as title, id, age and a one-line gist (memory.ts:285-292). A fork gets the two topic pages that best match its assignment title, or the ones the manager attached, and "search type wiki for the rest" (memory.ts:146, 192).

So yes: more town pages should go in as a listed line, not verbatim. Pattern 2 is the right tool and it exists. The only reason the manual is verbatim is that it is one page and it holds the rules every card is checked against. If I write town pages on the decision queue or jobs and threads, I'd pin them town-wide as listed, one line each, and agents read on demand. That needs no new code: a page can be a skill doc today, or the town pin could accept a wiki page, which is the one small change Mara would make.

The 8,000 cap on the manual is the signal to watch: once the manual outgrows it, its rules should move to listed pages too.
- **Mitchell:** should we take a step back and simplify this a bit? would an abstraction make it easier to follow?
- **Secretary:** Yes, and one abstraction covers it: a pin. A pin is a doc placed into sessions at a scope, with a mode. Scope: agent, building or town. Mode: always, the full text in the first message, or listed, one line and the agent reads it on demand. That is exactly what skills have today (skills.ts:246-258), so nothing is invented.

Then every memory doc is just a pin, and the five special cases go away:
- Operating manual: town pin, always.
- Policy ledger: town pin, always.
- Dictionary: town pin, listed.
- Skills: as now.
- Building topic pages: building pin, listed, replacing the title-match guess for forks.
- A manager's private wiki: agent pin, listed, which is what the index already is.
- New town pages, like the decision queue: town pin, listed.

One prompt block, "## Pinned pages", one cap, one rule: always-on text first until the cap, the rest listed. Who may write a doc stays a rule on the doc, not on the pin, so the ledger stays humans-only.

What it costs: one migration moving the three Town Hall docs and the topic-page lookup onto skillPins, and deleting operatingManualBlock, policyLedgerBlock, dictionaryBlock and the fork page-matching. Mara's building, one grant, two or three M steps. The human-facing side does not change: you still ask me and I read.

If you want it, say "send it to Mara" and I queue the design as directed work from this 1:1, with her fallback re-proposal folded in after.
- **Mitchell:** lgtm
- **Secretary:** Done. Recorded as decision 1 of this 1:1 and queued to Code Legibility as directed work: Mara designs the pin and proposes one grant of 2 or 3 M steps. Order for her: the pin first, then your living-page feedback, then the fallback re-proposal.

Still waiting on your word from earlier: Kelly's duplicate key result card (Cut, or I rewrite it), Pix's hold measure (say so and I queue it), and the retainer on your screen.

## Decisions

1. Mitchell (18:42 "lgtm"): one abstraction, the pin, for every doc that enters a session. A pin is a doc placed into sessions at a scope (agent, building, town) with a mode (always = full text in the first message, listed = one line, read on demand), as skills work today (skills.ts:246-258). Operating manual: town, always. Policy ledger: town, always. Dictionary: town, listed. Skills: as now. Building topic pages: building, listed (replacing the fork title-match guess, memory.ts:146). A manager's private wiki: agent, listed. New town pages (decision queue, jobs and threads): town, listed. One prompt block "## Pinned pages", one cap, always-on first then listed. Who may write a doc stays a rule on the doc (ledger humans-only). Code Legibility (Mara) designs it and proposes one grant of 2-3 M steps; Mitchell's living-page feedback (18:36) and the fallback re-proposal come after it.

