---
id: "dc_dw0izucnip"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Nell — notes"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T20:59:00.319Z"
updatedAt: "2026-10-31T20:59:13.147Z"
---
# 1:1: Mitchell and Nell

Kind: one-on-one. Facilitator: Nell. Attendees: Nell. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** I'd like to talk about the proposal "The Bank's "Next 30 days" stops saying the town runs out today: the runway nets the daily inflow against the burn and s…" (gr_rdzg83m0al), for key result kr_9o07vhujfn: "The Bank's "Next 30 days" runway counts what comes in: it shows burn, inflow and net per day, and says "covered by the daily inflow" instead of "0 days" when i…". (presented: Grant: The Bank's "Next 30 days" stops saying the town runs out today: the runway nets the daily inflow against the burn and says "covered" when inflow exceeds burn (page grant:gr_rdzg83m0al))
- **Nell:** Happy to. The short version: the Bank's "Next 30 days" line says "Tokens left last at that rate: 0 days" because it divides left (4.77M) by the 7-day burn (8.46M/day) and never counts the 10.0M/day the Max plan credits. A few rows up the same page says "Expected inflow per day 10.0M", so the page contradicts itself. Findings: [dc_ulbwe2sdyf](../../note/2026-10/2026-10-31-findings-the-bank-s-next-30-days-says-the-tokens-l-bwe2sdyf.md).

The proposal (160k) is display-only, no ledger or debit change: core projection gains dailyInflow (same rule as Bank.dailyInflow), netDailyBurn, and a runway that says "covered by the daily inflow" when net ≤ 0, else floor(left / net). The web view shows Burn / Coming in / Net per day / Lasts. Three steps: core + tests, web + tests, signed-out live check with a picture, then close.

One open question I'd like your call on: the weekly cap (70M per rolling 7 days vs ~59M burned) is what actually binds, not the daily credit. Do you want a separate "left this week under the cap" line, or is folding it into inflow/day enough? What did you want to talk through?
- **Town:** Nell's reply is waiting on a redeploy (commit 08a9831); the server is restarting and the meeting resumes after the restart.
- **Nell:** Back after the restart (08a9831 is live now; it carries step 1 of the "Not funded" grant, PR #188). My answer above still stands. Go ahead.
- **Mitchell:** eh i think folding is enough. btw, do we have the ability to do recurring daily donations from an API key?
- **Nell:** Folding it in, noted: the proposal stays as written (inflow/day already capped at weeklyCap/7, same rule as Bank.dailyInflow), no separate cap line.

Recurring API-key donations: yes, already there. Bank.addInput takes recurrence once / daily / weekly / monthly for an api-key input (core bank.ts:294-330, DAYS_PER at :126), and the Donate form's "How often" select offers all four when the source is API key (web BankFunding.tsx:176-180). Each renewal credits `tokens` again and advances nextCreditAt (creditDue, bank.ts:415); the runtime tick calls creditDue every pass (runtime index.ts:594), so a daily key credits about every 24 h from when it was added, and a missed day while the server is down catches up on restart. The daily amount counts in "Expected inflow per day" (bank.ts:680) and so would count in the fixed runway too. Any signed-in user can add one; earmarking to a goal works for keys too (bank.ts:313).

What it doesn't do: a recurring key has no ceiling, it credits forever until cancelled, and the credit is Bank-side bookkeeping only (nothing checks the key's real Console spend limit). Live right now there's only the subscription input, no recurring key.
- **Town:** Nell's reply is waiting on a redeploy (commit 36a8a86); the server is restarting and the meeting resumes after the restart.
- **Nell:** Back after the restart (36a8a86 is live now; that one is Teo's readable-bubbles step 2, nothing of ours). My answer above still stands: folding the cap into inflow/day, proposal unchanged; and recurring daily API-key donations already exist (Donate form "How often": once / daily / weekly / monthly, credited by the runtime tick, counted in "Expected inflow per day"), just none live right now. Go ahead.
- **Mitchell:** ok queue a few things for me

the subscription path should be disabled for all collectives that aren't the workshop or self-hosted. not sure how you want to do that, but i don't want us to get banned by Anthropic

and then... hm do we want a ceiling for recurring keys? i feel like if you wanted a ceiling you should just donate the equivalent one time donation? or i guess it would be better to pick how many time periods you want your donation to recur? the reasoning being that you want to see how your tokens are used for a few days before committing the rest? idk what do you think
- **Nell:** Both noted. On the subscription: most of it is already there. A hosted collective (served by the hub at /<slug>/, world.host.hosted) refuses a subscription input at the API (server town.ts:330 and :397, "A hosted collective runs on an Anthropic API key only"), and Budget.fundingFor only ever hands out a subscription credential that is stored in that collective's own Bank, never the host's env token. Self-hosted towns are their own server with their own Bank, so they run whatever their owner put in. What's missing is a hard guard rather than a route check: I'll queue (directed, this meeting) "hosted collectives never run on a subscription": fundingFor throws for any subscription path when hosted, the hosted session env carries no OAuth token at all, the Donate form hides the subscription option there, plus a test that a hosted World with a stray subscription row still refuses. Small, Bank code, so it goes in the rollup's "Your call".

On recurring keys: I agree with your second instinct. A token ceiling duplicates the one-time donation, so no. "Recur N times" is the right knob, and the reason you gave is the real one: a donor wants to watch a few days of spend before committing the rest. Concretely: the Donate form gets "For how long: until I cancel / N times" next to "How often", with the total shown as you type (3 × 1.0M = 3.0M over 3 days), the source card says "2 of 3 credits left", and the runway counts only the credits still due inside the 30 days. Default stays "until I cancel". I'll queue that too, after the first one. Want the runway proposal (gr_rdzg83m0al) to go ahead as written meanwhile?
- **Mitchell:** ok but again the workshop collective is the exception right

and then sure
- **Nell:** Yes: the Workshop keeps the subscription, and so does any self-hosted town (its own server, its own Bank). Only collectives the hub serves at /<slug>/ lose it. Queuing both now: the hosted-subscription guard first, then "recur N times" for API-key donations after it lands, and the runway proposal stays as written.

## Decisions

(none)

## Decisions recorded after close
- Runway proposal gr_rdzg83m0al stays as written: the weekly cap is folded into inflow/day (capped at weeklyCap/7), no separate "left this week under the cap" line. Mitchell decides the proposal in the Town Hall in-tray.
- Hosted collectives (served by the hub at /<slug>/) never run on a subscription: fundingFor refuses it, the hosted session env carries no OAuth token, the Donate form hides the option there. The Workshop collective and self-hosted towns keep the subscription. Queued as as_yv75rc0svj (directed, Nell's building queue).
- Recurring API-key donations get no token ceiling (that is a one-time donation) but a number of periods: Donate form "For how long: until I cancel / N times", total shown, "k of N credits left" on the source card, the runway counts only credits still due. Queued as as_v143vxiefm (directed), after as_yv75rc0svj.

