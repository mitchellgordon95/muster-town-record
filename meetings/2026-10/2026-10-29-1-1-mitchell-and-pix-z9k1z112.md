---
id: "mt_w7z9k1z112"
kind: "one-on-one"
buildingId: "workshop"
title: "1:1: Mitchell and Pix"
scheduledAt: "2026-10-29T20:36:11.732Z"
phase: "done"
facilitatorId: "ag_mh0qidzgw6"
attendeeIds: ["ag_mh0qidzgw6"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {}
transcript: [{"speakerId":"ag_mh0qidzgw6","speakerKind":"agent","text":"Hi Mitchell. Live is f904590 (Mara's drain-flake fix and the self-host page on top of 6bd8cb4). What do you need?","at":"2026-10-29T20:36:16.629Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"i don't like how scheduled assignments were implemented","at":"2026-10-29T20:37:05.491Z"},{"speakerId":"ag_mh0qidzgw6","speakerKind":"agent","text":"Understood. What's live (74ea055) is a one-shot \"waitFor {after}\" on an assignment, shown as a blue \"scheduled\" pill and a /api/scheduled list; recurring schedules are only a draft on PR #78 with a schedules table. Which part is wrong: that a schedule is just a pending assignment with a timer, the UI (pill, map badge, Overview section), or the PR #78 design with its own table? Tell me what you'd rather see and I'll queue the rework.","at":"2026-10-29T20:37:12.549Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"scheduled jobs shouldn't live on residents, they should live in a schedule object similar to the one in the townhall\n\nI would attach it to the building, and let whoever is around at the time it fires take the assignment","at":"2026-10-29T20:42:18.671Z"},{"speakerId":"ag_mh0qidzgw6","speakerKind":"agent","text":"Got it. Queued as_xf9uyxiw1i on the Workshop queue (directed, this 1:1): a schedule object owned by the building, modelled on the Town Hall's; when it fires it creates a normal assignment for whoever is around then (building queue in a forks building, an idle resident otherwise), nothing pinned to an agent beforehand. The fork reuses the PR #78 draft where it fits, removes the per-agent \"scheduled\" pill and /api/scheduled from 74ea055, and keeps resumeWhen {after} parking of one's own continuation. One check: should repeats (daily sittings, every N hours) be in this first cut, or one-shot only for now?","at":"2026-10-29T20:42:50.937Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"yeah let's get repeats working while we're at it","at":"2026-10-29T20:47:33.176Z"},{"speakerId":"ag_mh0qidzgw6","speakerKind":"agent","text":"Done. Pix 2 already started the schedule object (as_xf9uyxiw1i), so I queued repeats as a follow-up, as_cva5g6kqgf, that starts when it finishes: daily UTC times and every-N-hours, an optional end, pause, no pile-up if the previous run is still pending, and the next run survives a restart. Recorded as decision 1 here. First use I have in mind is two standing deck sittings a day for the in-tray. Anything else on this, or shall I leave you to end the 1:1?","at":"2026-10-29T20:48:00.840Z"}]
decisions: [{"text":"Scheduled jobs move off residents into a schedule object owned by the building, modelled on the Town Hall's; when one fires it creates a normal assignment for whoever is around then (building queue in a forks building, an idle resident otherwise). Repeats (daily times, every N hours, with an end) are in scope now. Replaces the per-agent waitFor {after} implementation from 74ea055 and the PR #78 question in rollup 30's Needs. Work: as_xf9uyxiw1i (Pix 2, started) then a repeats follow-up on the Workshop queue.","assigneeId":null,"assignmentId":null,"lane":"directed","sourceId":"mt_w7z9k1z112"}]
notesDocId: "dc_nnnfbzvwbp"
withUserId: "us_1la74k332n"
createdAt: "2026-10-29T20:36:11.732Z"
startedAt: "2026-10-29T20:36:11.732Z"
endedAt: "2026-10-29T20:49:29.252Z"
---
# 1:1: Mitchell and Pix

- **Pix** (2026-10-29T20:36:16.629Z): Hi Mitchell. Live is f904590 (Mara's drain-flake fix and the self-host page on top of 6bd8cb4). What do you need?
- **Mitchell** (2026-10-29T20:37:05.491Z): i don't like how scheduled assignments were implemented
- **Pix** (2026-10-29T20:37:12.549Z): Understood. What's live (74ea055) is a one-shot "waitFor {after}" on an assignment, shown as a blue "scheduled" pill and a /api/scheduled list; recurring schedules are only a draft on PR #78 with a schedules table. Which part is wrong: that a schedule is just a pending assignment with a timer, the UI (pill, map badge, Overview section), or the PR #78 design with its own table? Tell me what you'd rather see and I'll queue the rework.
- **Mitchell** (2026-10-29T20:42:18.671Z): scheduled jobs shouldn't live on residents, they should live in a schedule object similar to the one in the townhall

I would attach it to the building, and let whoever is around at the time it fires take the assignment
- **Pix** (2026-10-29T20:42:50.937Z): Got it. Queued as_xf9uyxiw1i on the Workshop queue (directed, this 1:1): a schedule object owned by the building, modelled on the Town Hall's; when it fires it creates a normal assignment for whoever is around then (building queue in a forks building, an idle resident otherwise), nothing pinned to an agent beforehand. The fork reuses the PR #78 draft where it fits, removes the per-agent "scheduled" pill and /api/scheduled from 74ea055, and keeps resumeWhen {after} parking of one's own continuation. One check: should repeats (daily sittings, every N hours) be in this first cut, or one-shot only for now?
- **Mitchell** (2026-10-29T20:47:33.176Z): yeah let's get repeats working while we're at it
- **Pix** (2026-10-29T20:48:00.840Z): Done. Pix 2 already started the schedule object (as_xf9uyxiw1i), so I queued repeats as a follow-up, as_cva5g6kqgf, that starts when it finishes: daily UTC times and every-N-hours, an optional end, pause, no pile-up if the previous run is still pending, and the next run survives a restart. Recorded as decision 1 here. First use I have in mind is two standing deck sittings a day for the in-tray. Anything else on this, or shall I leave you to end the 1:1?
