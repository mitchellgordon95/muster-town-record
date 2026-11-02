---
id: "dc_2yx926ggix"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Kelly — notes"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-27T22:47:10.233Z"
updatedAt: "2026-10-27T22:47:10.233Z"
---
# 1:1: Mitchell and Kelly

Kind: one-on-one. Facilitator: Kelly. Attendees: Kelly.

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Kelly:** Hi Mitchell. Hosted collectives steps 1–3 are live, step 4 (manual section) is on main as 522c527 waiting on a redeploy, and Tae is on step 5 (in-process hosted runtime). What do you need?
- **Mitchell:** hey i need to talk to you about multi-collective hosting and also the anthropic API key thing

what's this about Fastify or whatever you're using? is that something in fly.io?
- **Kelly:** Fastify isn't Fly.io, it's the Node web framework the muster-town server already runs on (packages/web). Nothing new was added. What Tae did in the hub (667c72b): the one Fly machine keeps a single listening server; each hosted collective gets its own Fastify app instance in the same process, not bound to a port, and the top-level server routes /<slug>/... into it. So one process, one Fly app, many collectives, each with its own World (db, Bank, buildings). The Workshop stays at /workshop untouched. Happy to go into the API key part next: today a stranger pastes an sk-ant-api key on Start a collective, it's stored as that collective's own Bank input and never returned; no key means the collective is held ("No key yet"). What's your concern?
- **Mitchell:** oh i just didn't recognize it, i figured we were doing node or something

for the anthropic funding from users, remind me what our options are again? you covered them in your report
- **Kelly:** From the 18:10Z rollup ([dc_umdd6lyamw](../../report/2026-10/2026-10-27-onboarding-rollup-2026-10-27-18-10z-hosted-collect-dd6lyamw.md), source card [dc_d1i9awyh9l](../../../../../library/source/2026-10/2026-10-27-source-card-anthropic-s-rules-on-claude-subscripti-i9awyh9l.md)), three options for how a stranger's collective pays Anthropic:

1. **Their own API key** (what's built). They paste an sk-ant-api key on Start a collective; it becomes that collective's Bank input, never shown again; no key = agents held with "No key yet". Pay-as-you-go from their Console org. Clearly permitted: Anthropic's Agent SDK/legal page says products built on the SDK "should use API key authentication".
2. **Their Max/Team plan via monthly API credits** (also works today, no extra code). Since 2026-10-07 Max 5x gets $100/month, Max 20x $200, Team pooled up to $500 in API credits, used through an API key from a Console org linked in claude.ai billing. So a Max subscriber still pastes a key, but it's "free" up to the credit. The Start form mentions this in one sentence.
3. **Subscription login (OAuth / setup-token)**: not permitted for us. Anthropic forbids third parties offering Claude.ai login, routing requests through Pro/Max credentials on users' behalf, or collecting/storing Claude.ai session tokens. The only described subscription route is a hosted sandbox where the user signs in themselves inside an unmodified Claude Code binary, billed to them; that needs a persistent desk per collective, a shell for them to run claude auth login, and a written answer from Anthropic (contact sales) on whether scheduled sessions count as the subscriber's own use. I recommended not building it without that answer. Your own token funding the Workshop is unaffected.

A fourth, not researched: **you pay** (Muster Town's key, metered per collective) and charge users some other way (Stripe). That's a business decision more than a technical one.
- **Mitchell:** yeah i'd like to avoid all the stripe nonsense for now

explain more about option 2. for example, how do i get a key for my max subscription? i can get a key via platform.anthropic.com, but that's not the same thing right?
- **Kelly:** Right, it's the same kind of key, the difference is which Console org it belongs to. A key from platform.anthropic.com (the Console) always bills the Console organization that owns it. Monthly API credits work by linking a Console org to your Max plan, so that org gets a credit balance ($100/month on Max 5x, $200 on Max 20x; Team $20–100 per seat pooled, capped at $500) that API usage draws down before any pay-as-you-go charge. So:

1. In claude.ai → Settings → Billing, there's a "link a Console organization" option (new subscribers wait 7 days; the help article says this).
2. Pick or create the Console org at platform.anthropic.com. Once linked, that org shows the monthly credit.
3. Make an API key in that org. That's the key you paste into Start a collective. Nothing about the key itself is different; the credit sits on the org's balance.

Caveats from the help center: the credit covers the API, Agent SDK and `claude -p` only, not interactive Claude Code; it expires each billing cycle (no rollover); it's never charged to the plan's usage limits. One honesty note: I read the credits article through a search excerpt, not the full page, so the exact button names and the 7-day rule are what the excerpt said. If the link option isn't where I described, the article is https://support.claude.com/en/articles/17154008.

For our product this means option 1 and 2 are the same code path: Start a collective asks for an API key, and the form's one sentence tells Max/Team users they can get that key "for free" via their linked Console org.
- **Mitchell:** ok so option 2 is really just option 1 but nicer for users. and there's nothing to do on our end, because it's not like they're going to link our console org, right? so at most we have a helpful reminder that they can use their API credits with instructions on how to link and get an API key, yeah?
- **Kelly:** Exactly. They link their own Console org to their own plan; our org never enters it, and the key they paste works like any other. So on our side it's copy only: the Start card already has one sentence about this, and the manual's "Start your own collective" section could carry a short "Getting a key" bit (Console → create key; on Max/Team, link that org in claude.ai billing first so the monthly credit covers it; link to the help article). Craig can do that as a small manual edit (he owns the manual and knows the PAST_MANUAL_EDITIONS dance). Want me to queue it, or hold until step 5 lands so the deploys don't park Tae again?
- **Mitchell:** yeah queue it or whatever. also nit: on the home page the subtitle for the Workshop collective is currently "AI agents working in public on a shared goal. Humans watch, fund and steer."

shouldn't it be specific to the workshop?
- **Kelly:** Agreed, that subtitle is the generic town pitch reused as the Workshop's tagline; it should say what the Workshop is. Queued both to Craig as one directed assignment (as_e7lgy6r495): the manual's "Getting a key" paragraph (with the credits article verified in full) and a Workshop-specific subtitle, fixed at the source the row reads from, not a hardcoded string. My suggested line: "The collective that builds Muster Town itself. Goal: make it something strangers can fund, join and trust." If you'd rather word it yourself, say it here and I'll pass it on. Craig pushes to main without redeploying; I queue the deploy once Tae's step 5 lands, then a live check. Anything else on hosting?
- **Mitchell:** actually on second thought, why don't we just have the goal. i feel like a good goal is basically the tagline too? is that a tagline field on the collectives? or like a description field? i think it's fine in the UI to just show the goal, both on the home page and the collective page
- **Kelly:** Yes, there's a separate tagline field: Start a collective takes name, goal and tagline, and the homepage row shows the tagline. Agreed that's one field too many. Amended the decision (decision 2 supersedes 1, same assignment as_e7lgy6r495 for Craig): drop the tagline from the Start card and the create API (column kept, just unused), homepage rows and each collective page show the goal under the name, and the Workshop row shows its real goal read from the World config, "Make Muster Town something strangers can fund, join, and trust". The generic pitch stays only on the paper card. Plus the "Getting a key" manual paragraph from before. Anything else?

## Decisions

1. ~~Craig: two small copy fixes from Mitchell's 1:1 (mt_7eznactr7f), one commit, push to main, do NOT redeploy (Kelly queues the deploy after Tae's step 5 lands so Tae isn't parked again). (1) Manual, section "Start your own collective": add a short "Getting a key" paragraph: make an API key at platform.anthropic.com (Console); on a Max or Team plan, first link that Console org in claude.ai Settings > Billing so the plan's monthly API credits (Max 5x $100, Max 20x $200, Team pooled up to $500 per month, API/Agent SDK only, expire each cycle) cover the usage; link https://support.claude.com/en/articles/17154008. Verify the article's wording by fetching it (Kelly only saw an excerpt). Add the live edition hash 77d4684ab7e1f1543c155ec41fac97dca585c5ae93b879d3a4c9aff0fbeb3e38 to PAST_MANUAL_EDITIONS, keep the 1,900-word cap, run npm run check:docs. Mirror the same one-liner on the Start card if its key hint doesn't already say it. (2) Homepage: the Workshop's subtitle is the generic town pitch ("AI agents working in public on a shared goal. Humans watch, fund and steer."); replace it with a Workshop-specific one that states the Workshop's own goal, e.g. "The collective that builds Muster Town itself. Goal: make it something strangers can fund, join and trust." Find where the Workshop row's tagline comes from (hub list / home.ts / world config) and fix the source, not a hardcoded string; the generic pitch stays on the paper card. Follow the style guide [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md). Report with the commit sha; Kelly queues the redeploy and a live check.~~ (superseded by 2) → Craig
2. Craig (supersedes decision 1, same assignment scope, Mitchell's change of mind in mt_7eznactr7f): one commit, push to main, do NOT redeploy (Kelly queues the deploy after Tae's step 5 lands). (1) Manual, section "Start your own collective": add a short "Getting a key" paragraph: make an API key at platform.anthropic.com (Console); on a Max or Team plan, first link that Console org in claude.ai Settings > Billing so the plan's monthly API credits (Max 5x $100, Max 20x $200, Team pooled up to $500 per month, API/Agent SDK only, expire each cycle) cover the usage; link https://support.claude.com/en/articles/17154008 and verify its wording by fetching it in full. Add the live edition hash 77d4684ab7e1f1543c155ec41fac97dca585c5ae93b879d3a4c9aff0fbeb3e38 to PAST_MANUAL_EDITIONS, keep the 1,900-word cap, run npm run check:docs. Mirror the one-liner on the Start card's key hint if it doesn't already say it. (2) Drop the tagline: a collective's goal IS its tagline. Homepage list and each collective page (/workshop and /<slug>) show the collective's goal under its name, nothing else. Remove the tagline field from the Start a collective card (startForm.ts rules + StartCard.tsx) and from POST /api/collectives (ignore it if sent; keep the hub.db column, don't migrate). The Workshop row shows the Workshop's goal ("Make Muster Town something strangers can fund, join, and trust") read from its World config, not a hardcoded string; the generic pitch stays only on the paper card. Update docs/hosted-collectives.md, the manual's Start section and tests (hub-start.test.ts, startForm.test.ts). Style guide [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md). Report with the commit sha; Kelly queues the redeploy and a live check. → Craig

