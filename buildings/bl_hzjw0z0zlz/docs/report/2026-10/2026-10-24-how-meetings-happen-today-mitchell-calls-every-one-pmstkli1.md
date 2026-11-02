---
id: "dc_q9pmstkli1"
type: "report"
state: "building"
title: "How meetings happen today: Mitchell calls every one and decides 87% of reports himself; 9 gaps vs the Town Hall in-tray target"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_guoh97iq91","dc_7fmlr7bvc1","dc_k955hun6c4"],"urls":["https://muster.town/api/meetings","https://muster.town/api/events","https://muster.town/api/docs?type=report&limit=200"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Kelly's meetings report is approved. Next: a short design note for the meeting changes agreed today: summaries seeded from the previous meeting's notes and the"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-24T20:03:31.330Z"
sessionId: "se_rjncpll7gs"
assignmentId: "as_xv6fp1beh1"
costUsd: 3.43388395
tokens: 39105
turns: 34
createdAt: "2026-10-24T19:27:38.251Z"
updatedAt: "2026-10-24T20:03:31.330Z"
---
## What I did

Read the meeting code (`packages/core/src/meetings.ts`, `core/verbs/meeting.ts`, `runtime/meetings.ts`, the summary and facilitator prompts in `core/prompts.ts`) and the two Town Hall notes ([dc_7fmlr7bvc1](../../../../../library/meeting-notes/2026-10/2026-10-24-town-hall-town-hall-notes-mlr7bvc1.md), [dc_guoh97iq91](../../../../../library/meeting-notes/2026-10/2026-10-24-town-hall-town-hall-notes-oh97iq91.md)). Then pulled the live town's data from muster.town: all 28 meetings, the full event log (11,934 events back to 2026-10-20 00:16Z, so counts below are exact for the live DB), the 200 reports the API returns, and every building's in-tray. Raw JSON is at `/home/agent/research/meetings/` on my desk. No code changed.

## Findings

### How a meeting happens today (code)

- **Who can call one:** only a human with `meeting.facilitate` or `building.manage`, from the web (meeting-room table or the building's Meetings tab, "Call meeting", starts at once). There is **no agent verb** that creates a meeting. A per-building cadence (`Building.meetings`, `everyMinutes`) exists in the scheduler, but every building's cadence is empty, so nothing fires on its own.
- **Attendees:** a lab meeting invites its residents (stopped ones too). A town-hall meeting invites every lab's manager and reviewer plus town moderators (today: Pix, Kelly, Cleo). Facilitator = the building's `managerAgentId`; for the Town Hall, the first active attendee.
- **Flow:** collecting → each attendee gets a Haiku one-shot summary (Did / Next / Need) built from its **own last report and last 20 events**; the last summary in starts the discussion → the facilitator runs an Opus session (≤60 turns, listen/speak loop; an @mention gives an attendee a no-tools reply, ≤5 per meeting) → `decide` (1-5 decisions; each with an assignee becomes an assignment with `fromMeetingId`, and auto-approves that agent's pending reports as "superseded") → `end` writes a meeting-notes doc (lab: filing cabinet; town hall: library). The runtime closes it if the facilitator didn't. Agents may not end it while a human spoke in the last 5 min or is typing.

### What actually happened (live data, 2026-10-20 to 10-24)

| | value |
|---|---|
| Meetings | 28: 23 Workshop standups, 2 Onboarding, 1 Prod, 2 Town Hall (both 10-24) |
| Created by | Mitchell, 28 of 28 (`meeting.created` payload.by) |
| Mitchell spoke in | 22 of 28 |
| Agenda set | 0 of 28 |
| Duration | median about 3 min, range 0.1 to 13.8 min |
| Decisions | 127; 91 with an assignee (72%); 8 with `waitFor`; 8 amended |
| Those 91 assignments | 83 filed a report (50 stop, 33 continue), 5 still active, 3 cancelled |
| Assignments overall (222) | 89 from meeting decisions (40%), 112 by Mitchell directly or via review-continue (50%), 9 by manager `assign`, 12 system |
| Reports decided (199) | Mitchell 174 (all approve), Pix 13 (all automatic meeting supersedes), system 12 (stops), 1 pending (mine) |
| Manual `review` by any manager agent | 0 |
| Meeting cost | $6.52 of $143.73 total (4.5%): 93 summaries $0.06, 38 facilitations $5.78, 26 replies $0.68 |
| Facilitation sessions ending in error | 12 of 38 (32%); 3 decision sets recorded in the after-close grace window |

Reading: meetings are the main way work gets assigned (40% of all assignments, and they produce reports 91% of the time), but every one is triggered by Mitchell's click, and Mitchell is also the person acknowledging 87% of raw reports. That is the opposite of the waterfall he described. Cost is not the constraint; his attention is.

### What notes and decisions produce

- A decision with an assignee produces a real assignment, and that works well (83 of 91 reached a report).
- The notes doc is write-only. Nothing reads it back: the next meeting's summaries come from each agent's last report and events, the facilitator sees only the current meeting, and decisions are tracked to completion only via the assignment. The notes print "→ Kelly" as text; the link decision → assignment → report exists in the Meeting record but is shown nowhere.
- "Need:" lines in summaries are the only human-ask channel and are free text; nothing collects them. In today's two town halls the Needs (OVH box, who builds the 1:1) surfaced only because Pix read them aloud.

### Gaps versus the target (town hall meetings + manager rollups into a Town Hall in-tray, recursive drill-down)

1. **No rollup artifact.** Reports land in the author's building in-tray; nothing aggregates per building. The Town Hall has no in-tray place, and `GET /api/buildings/town-hall/intray` is empty by construction.
2. **Managers don't review.** All three buildings run `reviewPolicy: human`; the manager `review` verb was never used manually. The only automatic review path is the `reviewer` role, not the manager. Mitchell sees every raw report.
3. **No trigger but Mitchell.** No cadence configured, no agent-callable meeting, no state trigger (in-tray above N, a report with a Need, a grant checkpoint).
4. **Town-hall summaries are per-agent, not per-building.** The manager's summary prompt gets its own last report, not its building's in-tray, blockers or decisions. A town hall needs a building-level Did / Next / Need.
5. **Drill-down is not recursive.** Town Hall → nothing; building → in-tray shows *pending* reports only, so once acknowledged a report disappears from the surface into the cabinet; agent → Talk and Assignments. No view has the same shape at each level.
6. **Decisions have no visible outcome.** The Meeting record links `assignmentId`, but neither notes nor UI show whether a decision landed, was cancelled or produced a report.
7. **Needs are not collected.** Free text, never aggregated to the human.
8. **Facilitation reliability.** 32% of facilitation sessions ended in error (causes not investigated; the meetings still closed). If the town hall becomes the interface, this needs looking at.
9. **The existing design doesn't cover it.** The goal-directed budgets design ([dc_k955hun6c4](../../../../workshop/docs/article/2026-10/2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md)) adds proposals and checkpoints but says nothing about rollups, a Town Hall in-tray or town-hall summaries; Pix is reconciling it (as_e7x218ubds).

What I infer, for Pix's design rather than decided: the smallest shape that closes gaps 1, 2, 4 and 5 together is one rollup doc per building per cycle, written by the manager from its own in-tray after it has decided the reports, filed pending in a Town Hall in-tray until Mitchell acknowledges it, linking the reports it covers. The town-hall summary for a manager then *is* that rollup's Did / Next / Need, and a building's in-tray shows decided reports grouped under their rollup, which gives the recursion.

## What I need from you

Nothing needed. Pix owns the design that uses this (as_e7x218ubds).
