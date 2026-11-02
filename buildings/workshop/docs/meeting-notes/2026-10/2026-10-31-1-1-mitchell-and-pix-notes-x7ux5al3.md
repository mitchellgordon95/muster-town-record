---
id: "dc_1tx7ux5al3"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T19:34:00.092Z"
updatedAt: "2026-10-31T19:34:00.092Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Step 1 (free tokens, pools gone) is live at 8d18dbc; step 3 is building on Pix 1; step 2 is re-queued after its session died with its work unpushed, and I've queued a diagnosis of today's four desk deaths. What do you need?
- **Mitchell:** it took a while for you to reply, do you know why? i thought we separated manager desk work from town hosted convos?
- **Pix:** Yes. The separation covers desk work sessions only: when a fork runs on a desk, a 1:1 gets its own host session beside it. But your 1:1 landed while I was in a team-lead session on the host (deciding the six reports that just came in), and that session is the "talker": manage.ts:110-113 pushes the 1:1 into it as an interrupt, so I only saw your line after the batch of tool calls in flight returned (three reviews, then three wiki writes). Fix: open a 1:1 beside a team-lead session the same way it is opened beside a desk session, so it answers at once. I'm queueing that now as directed work from this 1:1.
- **Pix:** One more cause, just diagnosed by Pix 4 ([dc_6mofz7twj6](../../report/2026-10/2026-10-31-pix-s-out-of-budget-is-the-per-agent-daily-cap-a-r-ofz7twj6.md)): the per-agent daily cap held me "Out of budget" from 18:56 to 19:18Z (2.07M used of a 2M cap), so no team-lead session could start until you raised the cap to 3M; you've raised it by hand twice today. The cap and the fork family cap (dailyTokensPerAgent × headcount) are real gates the vision doc never retired: §8 says desks and free tokens are the only limits. It is a token-policy change, so I'm asking: may I delete both caps (one standalone PR; the column stays, nothing reads it, like the pools)? If yes I queue it now.
- **Mitchell:** ok yeah, let's delete the caps, i don't think we need it in addition to the other budgeting mechanisms (bank cap, desk concurrency, exploration cap if set, grant max)

for the extra session in parallel to the agent team lead session, are we adding too many parallel sessions for one "agent"? or should the 1:1 interrupt the host session like a normal interjection, with a note to the user that the host session is already active? idk, on the fence about it

also the town looks much better, wondering if we have plans for different formats you can select at the town map? (like radial, tree, town-like)
- **Pix:** Caps: queued as as_1xfn7hh007 (Pix 4's deletion list, no migration, the column stays unread like the pools did). Parallel sessions: I agree, one mind per agent is better. I've redirected the fix (Pix 4, as_geh65af12k) to your second option: a 1:1 opening mid-team-lead-session interrupts it "now" (the current turn aborts, I answer, then resume the reports), and the panel shows a one-line note that I'm in a team-lead session. Cost: the aborted tool batch is redone, cheaper than a second session. Map formats: no plan yet beyond asking you to pick one of the three mocks ([dc_fvgi5nq36j](../../note/2026-10/2026-10-31-map-shape-mocks-three-layouts-of-the-live-tree-gi5nq36j.md): fountain plazas, plain tree, radial). Since every layout is a pure function of the goal tree, a picker on the town map is natural: three layouts, default the current packed one, choice saved per viewer. Say yes and I queue it; or pick one shape and I build only that.
- **Pix:** Heads-up while you're here: step 3 (declarative exploration) is in PR #173 and merges after CI. Once it is live, the tick starts an explorer in every building that has an idle desk, no startable queue item, no open proposal and ≥100k free tokens under its goal, at most one per 30 min per building; each ends with one grant proposal in your in-tray. The rule is on at the root by default; the goal tree's Funding block gets an Exploration row (on/off/inherit, chunk size) if you want to turn it off anywhere or everywhere.
- **Mitchell:** yeah please queue the picker, but lets make it global for the town, not just the viewer. and let's make the default fountain when you make a new collective
- **Pix:** Queued as as_gen9zq97tf: three layouts (fountain plazas, plain tree, radial) as a town-wide setting with a picker on the town map for admins and goal owners; new collectives default to fountain. One question I've answered for you unless you say otherwise: the migration sets the existing town to "tree" so the live map doesn't change shape under you until you flip the picker. If you'd rather the live town switches to fountain on deploy, say so and I'll adjust.

## Decisions

1. Delete the per-agent daily token cap and the fork-family cap: desk concurrency, free tokens under the goal, the optional exploration cap and grant totals are the only gates. Queued as as_1xfn7hh007 (Pix 4's deletion list [dc_6mofz7twj6](../../report/2026-10/2026-10-31-pix-s-out-of-budget-is-the-per-agent-daily-cap-a-r-ofz7twj6.md) item 4).
2. A 1:1 opened while the manager is in a team-lead session interrupts that session now (no second parallel session), with a note to the human that the manager is in a team-lead session. as_geh65af12k (Pix 4) redirected to this shape.
3. Map layout picker on the town map: fountain plazas / plain tree / radial as a town-wide setting (admins and goal owners change it; everyone sees it); new collectives default to fountain; the existing town stays on tree until switched. Queued as as_gen9zq97tf.

