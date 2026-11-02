---
id: "dc_nnnfbzvwbp"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-29T20:49:29.250Z"
updatedAt: "2026-10-29T20:49:29.250Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Live is f904590 (Mara's drain-flake fix and the self-host page on top of 6bd8cb4). What do you need?
- **Mitchell:** i don't like how scheduled assignments were implemented
- **Pix:** Understood. What's live (74ea055) is a one-shot "waitFor {after}" on an assignment, shown as a blue "scheduled" pill and a /api/scheduled list; recurring schedules are only a draft on PR #78 with a schedules table. Which part is wrong: that a schedule is just a pending assignment with a timer, the UI (pill, map badge, Overview section), or the PR #78 design with its own table? Tell me what you'd rather see and I'll queue the rework.
- **Mitchell:** scheduled jobs shouldn't live on residents, they should live in a schedule object similar to the one in the townhall

I would attach it to the building, and let whoever is around at the time it fires take the assignment
- **Pix:** Got it. Queued as_xf9uyxiw1i on the Workshop queue (directed, this 1:1): a schedule object owned by the building, modelled on the Town Hall's; when it fires it creates a normal assignment for whoever is around then (building queue in a forks building, an idle resident otherwise), nothing pinned to an agent beforehand. The fork reuses the PR #78 draft where it fits, removes the per-agent "scheduled" pill and /api/scheduled from 74ea055, and keeps resumeWhen {after} parking of one's own continuation. One check: should repeats (daily sittings, every N hours) be in this first cut, or one-shot only for now?
- **Mitchell:** yeah let's get repeats working while we're at it
- **Pix:** Done. Pix 2 already started the schedule object (as_xf9uyxiw1i), so I queued repeats as a follow-up, as_cva5g6kqgf, that starts when it finishes: daily UTC times and every-N-hours, an optional end, pause, no pile-up if the previous run is still pending, and the next run survives a restart. Recorded as decision 1 here. First use I have in mind is two standing deck sittings a day for the in-tray. Anything else on this, or shall I leave you to end the 1:1?

## Decisions

1. Scheduled jobs move off residents into a schedule object owned by the building, modelled on the Town Hall's; when one fires it creates a normal assignment for whoever is around then (building queue in a forks building, an idle resident otherwise). Repeats (daily times, every N hours, with an end) are in scope now. Replaces the per-agent waitFor {after} implementation from 74ea055 and the PR #78 question in rollup 30's Needs. Work: as_xf9uyxiw1i (Pix 2, started) then a repeats follow-up on the Workshop queue.

