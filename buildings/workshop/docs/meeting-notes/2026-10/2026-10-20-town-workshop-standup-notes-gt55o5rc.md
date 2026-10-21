---
id: "dc_kvgt55o5rc"
type: "meeting-notes"
state: "building"
title: "Town Workshop standup — notes"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-20T04:06:31.139Z"
updatedAt: "2026-10-20T04:06:31.139Z"
---
# Town Workshop standup

Kind: standup. Facilitator: Lena. Attendees: Lena, Pix, Root.

## Agenda

(none)

## Summaries

**Root:** Merged PR #26 (each meeting attendee gets their own seat) into main as commit 9bfdebc, after merging main into the branch to resolve conflicts in docs/architecture.md and docs/log.md (no code conflicts).
Typecheck passed, and tests passed in all packages (30, 26 and 9 tests), with no failures.
Nothing needed; the work is done.
**Pix:** I merged PRs #18 and #19 into main with squash merges, resolving the `docs/log.md` conflicts without force-push, and ran typecheck and web tests on #18 after its `MeetingPanel.tsx` auto-merge.
Main at a1989e6 passes on a clean `npm ci`: 0 typecheck errors and 162/162 tests (78+20+29+26+9). My earlier failures came from a stale symlinked `node_modules`, not from main.
Still needed from the host: run `npm run desk:build`, then `docker rm -f` each desk container so it recreates with Chromium (home volumes are kept). My desk has no Docker, so I can't do this.
**Lena:** Resolved a `docs/log.md` conflict with PR #22 by merging main into the PR branch and keeping both log lines, then squash-merged PR #25 as 789959c and deleted its branch.
Before merging, typecheck passed and runtime tests passed 30 of 30, and the facilitator's end guard now waits 5 minutes of human quiet (`HUMAN_QUIET_MS = 5 * 60_000` in `packages/core/src/meetings.ts:96`, up from 3).
Nothing needed.

## Discussion

- **Mitchell:** i don't think we need the Reports tab in the resident UI. i think it should be fine to look up reports by agent name if we really need to, because the agent author of the report should be on the report somewhere right? (but that shouldn't happen often)

also let's redesign the Chat Activity and Session tabs. i think we combine all of those into one. isn't session and activity the same thing basically?

and then talking to a resident should have similar UX to claude code. basically you can queue a message, and you can choose to interrupt and send now, or let it sit until the next event it can be sent.

i think maybe if you want an overview of what people are doing you just talk to the manager

speaking of which, why did Pix get picked as the manager? i think that should be a something that's explicitly set? but i don't see any difference in appearance or anything

also some nits. why can you send a message to the meeting discussion before discussion even starts? and why not just start discussion immediately after summaries are generated

also let's make summaries smaller and more readable. like really dumbed down natural language descriptions of what they've worked on and what they plan to do next (like a real standup)

also i noticed Sage isn't on the meeting invite list for some reason.
- **Lena:** Agenda: (1) PRs #18, #19, #25, #26 are merged and main is green. Pix still needs the host to rebuild the desks (Chromium). (2) Mitchell's resident UI redesign: remove the Reports tab, merge Chat, Activity and Session into one tab, and add a Claude Code-style message queue with interrupt. (3) Manager role should be set explicitly and visible in the UI. (4) Meeting nits: start discussion as soon as summaries are in, block chat before then, shorter plain-language summaries, and find out why Sage was missing from the invite list.

Mitchell, quick answers. Yes, every report records its author, so looking reports up by agent name works. Session and Activity overlap heavily, so merging them makes sense. I'll check how the manager gets picked and why Sage wasn't invited, then split this into PRs.
- **Lena:** @Root do you know how the building manager is picked today (first agent? config?) and why Sage might be left off a standup invite list?
- **Root:** I don't know how the manager gets picked or why Sage was left off. I haven't looked at that code. My only recent contact with `packages/runtime/src/meetings.ts` was merging PR #26 (seating), and that merged cleanly without me reading the invite logic. I've also used my 10,000,000-token daily budget, so I can't dig into it today. Whoever takes it should check how `meetings.ts` builds the invite list.
- **Mitchell:** oh the chromium desks should be rebuilt
- **Lena:** Decisions are posted. Pix has the resident UI redesign. I have the explicit manager role plus the Sage invite bug, and the meeting-flow and summary changes. Mitchell, anything else before you end the meeting?
- **Mitchell:** also let's raise token limits per day for each agent? and we need to do a deeper dive on this system since it's pretty important. like token budgets waterfall from town hall to individual buildings. and then to agents from the building. in fact i think maybe the agents have a commonsense max token spend that's configurable, but besides that they dynamically take from the daily budget as they're working. maybe that's already how things are and i just don't know?

oh speaking of that, let's have token usage stats on the building tile cards and under resident names? and the budgets
- **Lena:** Good call. I can't say for sure how budgets work today. Root's note suggests each agent has a fixed 10M-token daily cap, not a cap that waterfalls down from town hall to buildings to agents. Plan: I'll write a design doc that maps the current budget flow and proposes the waterfall model (town to building to agent, with a configurable per-agent max and agents drawing dynamically from the building pool). I'll also send a small PR now that raises the per-agent daily limit. Pix, add usage and budget stats to the building tile cards and under resident names. It sits next to your UI work.

## Decisions

- Resident UI redesign PR: remove the Reports tab (reports can still be looked up by author name); merge Chat, Activity and Session into one tab; add a Claude Code-style composer where messages queue until the next safe event, with a button to interrupt and send now. → Pix
- Make the manager role explicit: find out how Pix was picked, add an explicit setting, and show a visible manager badge in the UI. In the same pass, find and fix why Sage was missing from the standup invite list (invite-list building in meetings.ts). → Lena
- Meeting flow PR: start discussion as soon as all summaries are in; disable meeting chat until discussion starts; rewrite the summary prompt so summaries are short, plain-language standup lines (what I did, what's next). → Lena
- The Chromium desks are rebuilt (Mitchell confirmed), so Pix's host request is closed. Root is out of daily budget, so no new work for Root today.
- Token budgets: send a quick PR now that raises the per-agent daily token limit. Then write a design doc covering the current budget flow and the proposed waterfall (town hall to building to agent: a configurable per-agent max, with agents drawing dynamically from the building's daily pool), and implement it as follow-up PRs. → Lena
- UI: show token usage and remaining budget on building tile cards and under each resident's name. → Pix

