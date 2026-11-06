---
id: "dc_3906dic86q"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-05T21:09:28.396Z"
updatedAt: "2026-11-05T21:09:28.396Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Rollup 49 went out 6 min ago and grant A step 1 is running on Pix 1 — what do you need?
- **Mitchell:** i had another question about the fork caching

doesn't caching only work for the same model? so if a manager is running a system prompt, and then the fork gets a copy that's cached, it only matters if the fork is also fable, right? i mean if you have more than 1 fork then the second one gets the cache, which is fine but...
- **Pix:** Right: the cache is per model (and per key), so a Fable prefix never serves an Opus request. But manager→fork sharing was never on the table anyway: a fork on the building queue runs on the building's model, or the model `assign` picks (budget.ts:212: assignment.model ?? building.model), and a manager's team-lead session is sent bare, without the Claude Code preset (docs/prompt-caching.md:27-30), so its byte prefix differs from a fork's from the tools block on. Grant A's win is fork→fork within one building: today every fork writes ~20.8k fresh (name/id on line 1, live KR spend, board, wiki excerpt with "updated N min ago"), so even two forks of the same building on the same model miss each other. After A, the first fork in an hour pays the write and every later one on that model reads it; the 1h TTL refreshes on each hit, so a building that runs forks steadily keeps it warm. Where it buys nothing: a building that runs one fork an hour, or forks that alternate between model and cheapModel (two caches). The kickoff/checkpoint desk sessions on the manager are the same story among themselves (all Fable, 85.8k median). I'll have step 1's live check report the share of forks that hit, not just the write size.

## Decisions

(none)
