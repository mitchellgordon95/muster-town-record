---
id: "dc_1hmfrshoqs"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Planner — notes"
authorId: "ag_lywy3igvel"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-01T02:15:41.186Z"
updatedAt: "2026-11-01T02:15:41.186Z"
---
# 1:1: Mitchell and Planner

Kind: one-on-one. Facilitator: Planner. Attendees: Planner. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** Let's plan under the goal "Make Muster Town something strangers can fund, join, and trust" (gl_town).
- **Planner:** Ready. Quick read of the tree under gl_town before we draft anything:

- Fund (gl_fund) is thin: one objective (someone other than Mitchell funds a key result end to end), no building attached, no open key results.
- Join (gl_join) carries four children but its own text is about "Steer (goal-directed)", not joining. Looks like a leftover from a rename; worth an edit so the pillar reads as "join".
- Trust (gl_trust) is the deepest: three buildings plus backups, self-hosting, token accounting.
- Every key result in the tree is archived; no grant is open anywhere right now.

Which do you want to plan first: fill out Fund, fix Join's wording, or decide what the next grants under Trust should be? I'll draft one proposal at a time once you pick.
- **Mitchell:** Let's plan under the goal "Collectively funded: anyone can put tokens behind a goal, see what it will cost before they do, and choose who pays." (gl_fund).
- **Mitchell:** what do you think about this as a sub goal

Anyone can fund a collective with dollars paid to Muster Town, which distributes tokens via API keys
- **Planner:** Fund's text has three clauses. Here's where each stands, from the Workshop's reports ([dc_dl378i72pv](../../../../workshop/docs/report/2026-10/2026-10-31-goal-tree-step-7-funding-streams-is-live-on-de243c-378i72pv.md), [dc_ttzpizm053](../../../../workshop/docs/report/2026-10/2026-10-31-goal-tree-step-8-the-funder-filter-merged-85b106b-zpizm053.md)):

1. **"Put tokens behind a goal"**: mostly built. Earmarked streams are live since step 7 (de243c1): a donor can scope a key to one goal, and the Bank shows each stream and what it last paid for. The gap is who can donate: today a stranger needs an Anthropic API key or a subscription token. There's no way to put money in.
2. **"See what it will cost before they do"**: not built. The Donate form warns when a donation is below one session (p90 over 7 days), but no goal shows "this will cost about N tokens" before you fund it.
3. **"Choose who pays"**: built as draw order (grant, then nearest earmark, then general balance). The funder filter (step 8, 85b106b) shows a donor what their tokens ran.

The one child goal under Fund, ob_qieolu8bvs ("someone other than Mitchell funds a key result end to end"), is the proof of all three and has no open key result.

I'd propose at most two new children under gl_fund, and leave ob_qieolu8bvs as the proof:
- **Cost before funding**: every goal shows an estimate of what the next grant under it will cost, from real session sizes, before a funder commits.
- **Fund with money, not just a key**: a stranger can pay money at the Bank and have it become tokens, with no Anthropic account.

Want both, one, or something else first? The Bank is admin-gated, so whichever we pick, the grant would come from Bank Transparency (Nell) or the Workshop (Pix), and you'd fund it.
- **Planner:** I like it. It closes the real gap: today "anyone" means "anyone with an Anthropic key". Drafted as gp_7vos6z6ujw under Fund, with your wording.

Three things it implies, so you can decide if they're in or out:
- **Muster Town holds the keys.** Each collective gets a key Muster Town made and metered, instead of a donor's key. The Bank already stores one credential per stream, so a town-issued key is just another stream, with its daily limit set by what was paid.
- **Dollars need a rate.** The Bank counts adjusted output tokens. Paying in dollars means a published price per token (or per session) so "see what it will cost" works in dollars too. That's where this goal meets the cost-before-funding one.
- **Someone must take the money.** Stripe or similar, outside the town. That's a Prod and legal item, and the first real step.

Accept, edit, or cut from the card. If accepted, I'd say Bank Transparency (Nell) proposes the first grant: a town-issued key stream and a dollar price, with Stripe as a key result of its own. (presented: Goal proposal (add-goal): Anyone can fund a collective with dollars paid to Muster Town, which distributes tokens via API keys. (page goal-proposal:gp_7vos6z6ujw))
- **Mitchell:** how do i add desks to a goal? i don't see the button anywhere
- **Planner:** The button exists, but only on goals that already have a building. On the goal canvas, each attached building shows as a chip with − and + beside it (GoalCanvas.tsx:196). Fund has no building, so its box just says "no desks" with nothing to press.

To put desks on Fund today, two ways:
- **Attach an existing building**: open its panel, Settings, "Attached to", pick Fund. Bank Transparency is the natural one.
- **Make a new building**: Planning desk, Buildings tab, set Goal to Fund. It starts with the default desks and a manager.

Either way, the + then appears on Fund's box.

That's a gap in the "thin layer on goals" idea: an empty goal should just have a + that makes a building for you. Want me to record that for Pix? One line: "+ on a goal with no building creates one attached there, named after the goal, with 1 desk and a manager."
- **Mitchell:** yes please
- **Planner:** Recorded as decision 1, assigned to Pix as as_6oeaiigq5d: a goal with no building gets a + that creates one attached there (named after the goal, 1 desk, a manager), and then the normal − / + steps.

Meanwhile, for Fund right now: the proposal gp_7vos6z6ujw is still in the strip for you to accept, edit or cut. Once Fund has a building, that building's manager can propose the first grant under it.

## Decisions

1. Goal canvas: a goal with no building attached shows a + beside its "no desks" tag (town.manage_buildings). Pressing it creates a lab building attached to that goal, named after the goal's short text, with 1 desk and a manager made by default, then shows the usual − / + desk steps for it (GoalCanvas.tsx:187-202; same creation path as the Planning desk's Buildings tab). Follows 1:1 mt_n25udpflus decision 3 (buildings are a thin layer on goals). → Pix

