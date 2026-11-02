---
id: "dc_ioj81zkttf"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Kelly — notes"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-01T01:37:44.354Z"
updatedAt: "2026-11-01T01:37:44.354Z"
---
# 1:1: Mitchell and Kelly

Kind: one-on-one. Facilitator: Kelly. Attendees: Kelly. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** I'd like to talk about your report "Onboarding rollup 2026-11-01 01:17Z: the stranger's road from sign-in to member is honest and measurable (gr_fibsfwr4tz…" ([dc_glnso66daa](../../report/2026-11/2026-11-01-onboarding-rollup-2026-11-01-01-17z-the-stranger-s-nso66daa.md)). (presented: [Onboarding rollup 2026-11-01 01:17Z: the stranger's road from sign-in to member is honest and measurable (gr_fibsfwr4tz steps 1–3 live), README one-pool Bank wording live; the real round trip waits on a human; after-let-in proposal filed](../../report/2026-11/2026-11-01-onboarding-rollup-2026-11-01-01-17z-the-stranger-s-nso66daa.md))
- **Kelly:** Hi Mitchell. I have the rollup open. Short version: three things shipped and are live (honest guest/pending cards + the admin "asked to join" notice, the public join funnel at /api/join-funnel and on the Dashboard, and the one-pool Bank wording in the README/self-host/hosted docs). The one thing still open on that grant is the real round trip: a never-granted GitHub account signing in, asking to join, you letting them in, them saying something. That's the outbox request you have; the fork checking it resumes in about 20 hours. Separately, Kelly 1 found that a member you let in has no way to reach anyone, and the proposal for that (gr_58n37j410s) is in your in-tray. What would you like to talk about?
- **Mitchell:** i like these, although i've been wanting to nuke the dashboard page. i never really asked for it, and i don't know what it does. what does it look like for other collectives? and the building goals are out of date, we have a goal editor
- **Kelly:** Here's what the Dashboard is, from the code (packages/web/src/panels/DashboardPanel.tsx, GET /api/kpis in routes/grants.ts). It came in with migration 043 as the "Objectives and KPIs" idea, not from anything you asked for. Three parts:
1. Three KPI tiles, Fund / Join / Trust, computed live over 7-day windows with an 8-week sparkline (strangers only; anything an admin does is excluded). Framing text on top quotes the town goal word for word.
2. "Building objectives": each building's goal plus its objectives and their key results, read from the old `set_objective` table. That's the stale part you noticed: the goal editor and grants are the source now, and objectives there are dead weight.
3. Our join-funnel row (added last night), which is just a summary of the public JSON.

For a hosted collective it's the same page with their own numbers, and it's a bit embarrassing: Hollyville's Dashboard says "The town goal, 'Make Muster Town something strangers can fund, join, and trust'…" because the framing string is a constant, not their goal. Their KPIs are all zeros, objectives are empty, and the funnel row shows only their slug.

My recommendation: nuke the page and the objectives section with it. The funnel JSON stays public at /api/join-funnel either way (that's the key result), and if you want one visible row of it I'd put it on the Bank or Finance page rather than keep a page for it. If you say go, I'll queue it as directed work from this 1:1: remove the Dashboard panel, its HUD entry and the objectives block from GET /api/kpis, keep the funnel endpoint. Want the KPI tiles gone too, or kept somewhere?
- **Mitchell:** yeah kill the kpi tiles. maybe user stats lives somewhere in the town hall on its own object. maybe we make the outbox table smaller to make room
- **Kelly:** Done, queuing it as directed work from this 1:1, two pieces:
1. Remove the Dashboard page: the panel, its HUD entry, the KPI tiles and GET /api/kpis, plus the "building objectives" block. The kpis table stays (dropping it buys nothing). The join-funnel JSON stays public.
2. A "User stats" object in the Town Hall, like the in-tray and outbox are objects: walk up, E opens a small panel with the join numbers (guest-card views, sign-ins, asked, let in, declined, typical wait, by day and per collective; later the "acted" count if you fund gr_58n37j410s). Outbox table shrunk to make room. Hosted collectives get the same object with their own numbers.

One assumption to check: by "user stats" I'm taking the join funnel, not the old Fund/Join/Trust measures. If you want something else on it (members by role, who was active this week), say so and I'll add it to the brief. I'll queue the removal first and the Town Hall object behind it; you'll see both in the next rollup with pictures.

## Decisions

1. Kill the Dashboard page: remove DashboardPanel, its HUD entry, the Fund/Join/Trust KPI tiles, GET /api/kpis and the building-objectives block; keep the kpis table (additive) and the public GET /api/join-funnel. Queued on the Onboarding building queue (lane directed, source mt_ec2b7x80rg).
2. User stats live in the Town Hall as their own object (walk up, E opens a small panel with the join numbers by day and per collective); the outbox table is made smaller to make room; hosted collectives get the same object with their own numbers. Queued behind the removal (lane directed, source mt_ec2b7x80rg).

