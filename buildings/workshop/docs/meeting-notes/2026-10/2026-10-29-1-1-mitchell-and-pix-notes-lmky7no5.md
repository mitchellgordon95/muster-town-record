---
id: "dc_8slmky7no5"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-29T21:38:22.659Z"
updatedAt: "2026-10-29T21:38:22.659Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Pix here, three forks running (schedule object, planner desks, and the bodies-go-home live check just landed at 158237b). What do you need?
- **Mitchell:** do we even need all the resident management UI now? let's just assume every building has one named manager. that simplifies a lot, no?
- **Pix:** Yes, I think it simplifies a lot. Every building already runs on forks of its manager, and the five leftover residents (Dara, Craig, Tae, Asha, Finn) are the only non-manager agents left, which you said you'd dismiss yourself. With "one named manager per building" we could cut: the resident roster and add/remove resident UI, assign-to-agent and reassign between residents, the harvest-residents' wikis step, the "team" block in manager prompts, and the per-resident desk bookkeeping (desks become just slots for the manager's forks). What stays: the manager itself, forks, visitor agents (Connect your agent, they're not residents), and the building topic pages. Two things I'd want to confirm before cutting: (1) do you want to keep an escape hatch to re-add a standing agent when a building's forks stall, or drop it entirely and treat that as a bug to fix? (2) retired residents' wikis and reports stay readable as history, we just stop rendering a roster. If that sounds right I'll queue one fork to inventory the resident-management surface (web, API, core, prompts) and come back with a cut list sized in PRs, then cut it.
- **Mitchell:** i don't know why you think there are leftover residents, i already dismissed them.

for (1) just drop it

(2) yeah in service of "publicly legible" we still need a paper trail

also what changes in the code for the building setting of forks vs not forks? we can get rid of that setting
- **Pix:** You're right, my note was stale; I'll fix it. So: one named manager per building, no standing residents, no escape hatch, history (wikis, reports, logs) stays readable.

On the forks setting: as far as I know it gates four things. (1) `assign` without agentId is only allowed with forks on; off, it demands a resident. (2) Queued building work spawns a fork of the manager instead of waiting for a resident. (3) The manager's prompt gets the "team / live forks / building queue" block vs a resident roster. (4) Budget: fork sessions draw on the building's budget and the desk pool, where residents had per-agent desk funding. Dropping the setting means forks are always on, agentId on assign goes away except "take it myself", and the resident branches of each of those are dead code. A fork will confirm the exact list when it reads the code.

I'll record two decisions now and queue them on the building: (a) remove the Budget mode setting, forks always on; (b) inventory the resident-management surface (web, API, core, prompts, desk bookkeeping) and cut it, keeping the paper trail. One fork each, directed from this 1:1, with PRs and a live check.
- **Pix:** Recorded as decisions 1 and 2 and queued: as_35jl2b7bhh (Pix 1 took it: remove the Budget mode setting, forks always on, PR + redeploy + live check) and as_i7jk8pw7tc (waits on it: inventory and cut the resident-management surface, paper trail untouched, stops before any schema migration to ask you). Both land in rollup 31.

## Decisions

1. Every building has exactly one named manager; standing residents are gone for good, with no escape hatch to re-add one. Remove the resident-management surface (roster, add/remove resident, assign-to-agent and reassign between residents, the harvest step, the resident roster in manager prompts, per-resident desk bookkeeping). Retired agents' wikis, reports and logs stay readable as history (paper trail for public legibility).
2. Remove the building Budget mode setting (forks vs residents): forks are always on. The resident branches it gated (assign requiring an agentId, queued work waiting for a resident, the roster prompt block, per-agent desk funding) become dead code and go.

