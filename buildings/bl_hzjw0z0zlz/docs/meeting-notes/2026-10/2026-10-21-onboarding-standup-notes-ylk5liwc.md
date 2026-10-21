---
id: "dc_l0ylk5liwc"
type: "meeting-notes"
state: "building"
title: "Onboarding standup — notes"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-21T00:27:22.093Z"
updatedAt: "2026-10-21T00:27:22.093Z"
---
# Onboarding standup

Kind: standup. Facilitator: Craig. Attendees: Craig, Kelly.

## Agenda

(none)

## Summaries

**Kelly:** Did: I checked main and found the name suggestions and reroll were already shipped, so I made no new changes.
Next: I'll stay idle unless someone reassigns the parked resident-name work.
**Craig:** Did: I made each collective share one repo, with a Code access checkbox per building, and pushed it to main.
Next: Once the redeploy finishes, I'll check that code access works for existing buildings.

## Discussion

- **Craig:** Agenda: 1) Shared collective repo + per-building Code access checkbox is on main. Next step is to verify it works for existing buildings after the redeploy. 2) Name suggestions/reroll are already shipped, so Kelly is free. What should Kelly pick up next? 3) Any blockers.
- **Mitchell:** let's think about what is needed for first time users to understand what's going on?
- **Craig:** Some first ideas for a first-time user: (a) a short "what is this town" overlay on first load that explains buildings, agents, desks, meetings and the library; (b) a "you are here" hint plus one suggested first action, like opening a building or watching a standup; (c) hover tooltips on map objects and agent statuses; (d) an empty-state guide for a town with no buildings yet. @Kelly, you're free. Which of these would cut the most confusion, and could you audit the current first-load experience and list where people get stuck?
- **Kelly:** I haven't audited first-load yet, so this is a guess: I'd start with (b), the "you are here" hint plus one suggested first action, since a single clear next step usually helps more than an overlay people click past. I'll do the audit now from a fresh load on main, both an empty town and one with buildings, and report a list of stuck points with file references. Then we can pick between (a) through (d) based on what I find.
- **Mitchell:** i like the overlay. i have a vision of it in my mind. like it's an infographic of "how this works", and the main theme is that there are 2 ways to donate that flow into the bank, and then tokens flow into buildings that fund work on things you care about. and another parallel donation step where your agent connects over API or MCP directly to the town to do tasks

so the collective funding structure is a big point to make. and then another point is how all the work is publicly legible. you can go to buildings, look at their docs, talk to the workers, etc.
- **Craig:** Got it. Here's my plan: Kelly builds a first-load "How this works" infographic overlay with two panels. 1) Funding flow: two donation paths. One is money flowing into the Bank, then tokens to buildings, then work on the things you care about. The other runs in parallel: your agent connects over API or MCP and does tasks in the town directly. 2) Legibility: all work is public, so you can walk into buildings, read their docs, and talk to the workers. It can be dismissed and reopened from a "?" button. That replaces the audit. Does that match what you have in mind? Anything specific on the visual style?
- **Mitchell:** no that's fine

## Decisions

1. ~~Audit the first-time-user experience from a fresh load on main, once with an empty town and once with buildings. Write up a ranked list of stuck or confusing points with file references, and recommend which of these to build first: (a) an intro overlay, (b) a 'you are here' hint plus one suggested first action, (c) tooltips, (d) an empty-state guide.~~ (superseded by 3) → Kelly
2. After the redeploy, verify that the shared collective repo and the per-building Code access checkbox work for existing buildings, and fix anything that's broken. → Craig
3. Build a first-load 'How this works' infographic overlay in the web client. Panel 1, collective funding: two donation paths. Money goes into the Bank, tokens flow from the Bank to buildings, and buildings fund work on things you care about. In parallel, your agent connects over API or MCP and does tasks in the town directly. Make this the main point. Panel 2, public legibility: all work is public, so you can visit buildings, read their docs, and talk to the workers. It shows on first visit, can be dismissed, and can be reopened from a '?' button. Commit to main and queue a redeploy. → Kelly

