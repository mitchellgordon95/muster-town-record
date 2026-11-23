---
id: "dc_qo6egjhlc0"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Secretary — notes"
authorId: "ag_7tiwyqva83"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-23T16:46:01.163Z"
updatedAt: "2026-11-23T16:46:09.783Z"
---
# 1:1: Mitchell and Secretary

Kind: one-on-one. Facilitator: Secretary. Attendees: Secretary. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Secretary:** Hi Mitchell. The queue has 14 open asks: two policy at the top, eleven money, one redeploy click. What do you need?
- **Mitchell:** don't we already have overrun buffer for these?
- **Secretary:** No buffer, only the session in flight. The code holds a grant exactly at its ceiling (packages/core/src/grants.ts:26-38; docs/legible-delegation.md §7.3 point 3: "at the ceiling it holds, and only there"). The one session already running finishes and books, which is why you see 251k of 250k. But no new session may start past the ceiling, so the live check, which is its own session, always trips the gate and files an adjust ask. The step-report forecast records "over ceiling" on the grant too, but by your 2026-11-17 decision it files no ask. This rule would let the town adjust by one S step once, only when every key result is claimed and just that check is left, and note it on the thread. Reversing it is one withdrawn ledger line.
- **Mitchell:** seems like a weird exception to carve out, shouldn't we just let the weekly step size approximation do its job? i just signed off on that in the last card
- **Secretary:** Fair. The design says the same: when grants hold before done, the fix is to raise a size, not to add a gate rule (docs/legible-delegation.md §7.4 table, line 223). Two things against the carve-out that I did not weigh on the card: it hides the signal the calibration reads, since auto-adjusted grants no longer count as held before done, so the Planner's line would stop tripping even if 55k is still too low. And it is a second rule where one lever already exists. One caveat: the 55k price only applies to grants funded from now on. The six adjust asks already in the queue were priced at 50k and still need your button each. If you want it, say "skip it" and I will press Skip on this card as you.
- **Mitchell:** oh and btw, the approximation should also reduce token size of step types if appropriate, right? i mean right now we're obviously under
- **Secretary:** Yes, it lowers too: a size whose completed steps spend under 0.7× its price over at least 30 steps gets a "Lower" proposal (packages/core/src/planner.ts:23-26, 75-79). But when the only line crossed is hold share or adjust asks per grant, it only raises the hottest size or splits L, never lowers (planner.ts:81-83). That is what fired this week.

One catch you should know. Adopt applies the code's computed number, not the card's words (planner.ts:204-209). The computed change rounds to the nearest 10,000 (planner.ts:46), and the thread entry at 04:06 reads "Raise S from 50,000 to 50,000 tokens". So the S ratio was under 1.1, the rounding ate it, the Planner wrote 55,000 on the card by hand, and your Adopt changed nothing. S is still 50,000. If you want S at 55,000 for real, that is PUT /api/town/defaults, an admin edit of the table. I will tell the Planner the card misstated the number.
- **Town:** Secretary's reply is waiting on a redeploy (commit ae5fd33); the server is restarting and the meeting resumes after the restart.
- **Mitchell:** for this one, both steps are good. should we make it so the residents can read the fly logs for the town app? and we can add swap that's fine

what does "building the web app in CI" mean?
- **Secretary:** Back after the restart.

"Building the web app in CI": today the town Machine itself runs `vite build` on every self-pull redeploy (packages/runtime/src/redeploy.ts:346). That is the 480 MB spike that likely froze it. CI already runs the same build to check it compiles (.github/workflows/ci.yml:49) but throws the output away. Building it in CI means CI keeps the built files (an artifact, or baked into the image) and the Machine only downloads them, never runs vite. Cleo sized that M to L, so it is not in this 100k.

Swap: Cleo left it out only because changing swap_size_mb in fly.town.toml triggers CI's image deploy, which replaces the Machine: one more unclean restart. If you are fine with that, it is the cheapest real fix and belongs in step 2, timed when few sessions run.

Fly logs: yes, worth it. The OOM line is in `fly logs -a muster-town`. The desk token gets "unauthorized" on that app, and Wright has no flyctl or token. The only way is a read-only Fly token you mint and store as a server secret. That is a credential ask, which Prod files, you decide once.

Two ways to do it: say "fund it" and I press Fund as you at 100k now, then tell Cleo swap is in and to file the token ask. Or say "counter" and I send it back with your words so Cleo rewrites step 2 with swap first. I recommend fund: the steps stand, swap fits in step 2 without more tokens.
- **Mitchell:** fund
- **Town:** Secretary did this for Mitchell: fund gr_xgr8j2f9ao ("Redeploys survive a full-memory town Machine"), now funded. Citing: "fund"
- **Secretary:** Done. Funded "Redeploys survive a full-memory town Machine" at 100k as you, quoting your "fund". Step 1 is on Prod's queue now. I told Cleo: swap goes into step 2 with the one Machine-replacing image deploy you accepted, timed for a quiet hour, and Prod files one credential ask for a read-only Fly token on app muster-town so a desk can run fly logs. Expect that card in your queue. Building the web app in CI stays out of this grant. Seven money asks are left in the queue.
- **Mitchell:** what's the command for this
- **Secretary:** fly tokens create readonly -o personal -n town-logs -x 8760h

"personal" is the org the deploy docs use (deploy/README.md:103). The readonly kind is the narrowest Fly offers: it reads every app in the org, including muster-desks, and cannot deploy, ssh or change secrets. 8760h is one year; shorten it if you prefer. Then paste the token as FLY_LOGS_TOKEN on the planning desk's Secrets tab, grant it to Prod, and press Set the token on the card. To check it before you paste: FLY_API_TOKEN=<token> fly logs -a muster-town --no-tail
- **Mitchell:** ok so i think this is a good idea, and it brings up something i was thinking about before

we've got like 3 knobs for priority and effort, right? exploration cap per goal (which right now is just set to inherit the root), fork concurrency, and number of  in-flight grants allowed, right? am i missing any?

anyways i think we tie all three to a single number that you can easily adjust on the goals tree. i think that number should probably just be "desks". then how desks translates to exploration budget, concurrent grants, etc. can be a setting with a default. but goals with more desks get more exploration budget, can propose and work on more grants in parallel, and as before, run more forks at once. thoughts?
- **Secretary:** Back after the restart. Checking the code for the knobs before I answer, one minute.
- **Secretary:** Checked. You are missing one and one of your three does not exist.

What the code has today: (1) desks: a building's headcount is its fork concurrency, and goals carry a desksTotal ceiling per subtree, combined as the minimum on the path to the root (free-tokens.ts:53-67; docs/goals.md:146-148, "Effort steering is desks"). (2) Exploration: three settings per goal, all inherited: on/off, the chunk size (100k default), and the daily cap (free-tokens.ts:27-46, 73-83). (3) Grants in flight: no limit anywhere. A building can have any number proposed or funded; the only throttle is your Fund button and the desks. Plus one global: the operating reserve.

So your idea is mostly the design already written down: desks are the steer, the tree says what matters, the Bank says how much. What is not done is deriving the other knobs from desks. Today the daily exploration cap is a flat 500k on the root, which is why Nell's card on your screen finds exploration capped 5 of 6 days while desks sit 99% idle.

My thoughts: yes, make desks the one number on the tree, and derive the rest from two town defaults: exploration tokens per desk per day, and proposals in flight per desk. Concurrency is already desks. Two cautions. One: today "desks" lives in two places, the building's headcount and the goal's desksTotal. Tie them: the goal's number is the truth and buildings under it share it, or you end up editing both. Two: a count of grants in flight is a new rule that mostly limits queue noise. You already fund each grant by hand, so I would start with exploration tied to desks and leave the grant count as a default of "no limit" until the queue shows a problem.

If you want it, say so and I will tell Pix to propose a grant for it, with this 1:1 as the source.
- **Mitchell:** yeah sgtm. and to be clear this should make simplify the goal editor UI by quite a bit
- **Secretary:** Told Pix, with this 1:1 as the source: one "desks" number per goal, exploration budget and grants in flight derived from it by town defaults, concurrency already desks, and that you want the goal editor cut down. Today a goal has four fields there: exploration on/off, chunk size, daily cap, desk total. With your idea it is one field, desks, and the defaults live once on the town settings page. Expect a Workshop proposal and its money card in your queue.

One thing on your screen now: the memory grant's adjust card, 100k more. It is there only because step one spent 88k against a 50k S price, the weekly calibration case we talked about. Step two is already running. Say "adjust" or "cut" and I press it as you.

## Decisions

(none)

## Decisions recorded after close
- Mitchell (16:35, 16:43Z): make "desks" the one steering number per goal on the goal tree. Fork concurrency is already desks. Exploration budget per goal and grants in flight per goal derive from desks by town defaults with a per-desk factor, editable once on the town settings. The goal editor drops its separate exploration fields (on/off, chunk, daily cap, desk total) to one desks field. Secretary told Pix (Workshop) to propose it as a grant with this 1:1 as its source (relay en_ev186627_relay); the money ask then goes to Mitchell's queue. Secretary's cautions, recorded: the goal's desks number should be the single truth over building headcount, and the grants-in-flight default should start at no limit.

