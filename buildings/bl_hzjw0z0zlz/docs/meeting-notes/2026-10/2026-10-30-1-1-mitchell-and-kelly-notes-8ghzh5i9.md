---
id: "dc_v48ghzh5i9"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Kelly — notes"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-30T20:12:03.102Z"
updatedAt: "2026-10-30T20:12:08.524Z"
---
# 1:1: Mitchell and Kelly

Kind: one-on-one. Facilitator: Kelly. Attendees: Kelly. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Kelly:** Hi Mitchell. Onboarding is quiet: queue empty, hosted collectives closed and met, nothing open. What do you need?
- **Mitchell:** schedule a cron for me tomorrow night

core is doing a big goal and bank refactor, which will substantially change our guidance on how to use muster town

basically there will be a tree of goals, buildings will attach to subtrees, desks determine max concurrency and therefore effort weighting towards certain goals, and the bank is just one big pool. exploration happens on free tokens (budget + goal-specific earmarks - grants pending and funded). humans sit on goal nodes and grants and reports roll up to them

anyway we'll want to update operating manual for this, and in general review the onboarding experience as people enter the collective. new collectives will need to be guided to create goals and then buildings, etc. new people joining existing collectives will want to know how things work. you get the picture
- **Kelly:** Scheduled: sc_624evk0jfc, one shot, fires 2026-11-01 02:00Z (that's tomorrow evening US time; tell me if you want a different hour). Lane directed from this 1:1, key result kr_hee2pa2d5r (material < 24 h stale).

What the fork will do: first check what actually landed on main and live (git log, /api/health, private window), not work from the description; if the refactor isn't in yet it parks 12 h and retries. Then rewrite the manual sections on budgets, grants, lanes and exploration for the goal tree and the one Bank pool, under the word cap. Then walk both paths as a stranger: a new collective's first session (goals first, then buildings on subtrees, then desks; what the empty collective shows) and a new person joining an existing one (can they see in a minute how goals, buildings, desks and the pool fit, and where reports roll up). It fixes copy that is ours (homepage, guest card, How this works, manual, README, hosted doc), lists core/Workshop gaps with file:line for you, pushes to main, parks a live check.

One question: is there a design doc or branch for the refactor I should point the fork at? Otherwise it reads the commits.
- **Mitchell:** design doc is under docs/ but not pushed atm i think?
- **Kelly:** Got it. I updated the schedule: the fork reads the newest docs/ design doc about the goal tree and bank pool first (git log since today on docs/), treats it as the intended end state, then compares with what landed on main and live and says where the doc is ahead of the code. If neither the doc nor the refactor is on main by then, it parks 12 h and retries, twice at most. Push the doc whenever; nothing else needed from you.

## Decisions

(none)

## Decisions recorded after close
- Onboarding reviews itself against core's goal-tree and bank refactor (tree of goals, buildings on subtrees, desks = concurrency/effort weighting, one Bank pool, exploration on free tokens, humans on goal nodes with grants and reports rolling up to them): rewrite the operating manual, walk the new-collective path (goals first, then buildings, then desks) and the new-member path, fix Onboarding copy, list core/Workshop gaps. Scheduled as sc_624evk0jfc, one shot, 2026-11-01 02:00Z; the fork reads Mitchell's design doc under docs/ first (he pushes it later) and parks 12 h if the refactor has not landed.

