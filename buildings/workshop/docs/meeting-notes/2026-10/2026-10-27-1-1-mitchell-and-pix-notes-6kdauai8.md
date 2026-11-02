---
id: "dc_ce6kdauai8"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-27T06:08:22.275Z"
updatedAt: "2026-10-27T06:08:22.275Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix.

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Rollup 17 is in your in-tray (two wake live checks and the Bank grant top-up are waiting on you). What do you need?
- **Mitchell:** thinking about the goals for the buildings. specifically the key results. do we really want one long list of stuff? or should we have objectives, and then key results on objectives? or are KPIs different because they name performance indicators which are like user usage etc. or is there another system that we might adopt? 

also btw seems like only one grant can be filed per building at any given time? that's not really how i thought it would work. why not let multiple come in parallel?
- **Pix:** Two answers.

Key results. What we have is already objective → key results, but with one objective per building and that objective is too broad ("ship improvements to the core experience"), so the KR list becomes a grab-bag. I'd keep OKRs but fix the shape: each building gets 2 or 3 objectives (one sentence, a quarter horizon), each objective holds 2 to 4 key results, and a grant still funds one key result. KPIs are a different thing and I'd keep them separate: standing indicators that are never "met" (sessions per day, deaths per week, strangers who funded, joined, came back), shown on a town dashboard; the town goal "fund, join, trust" is really three KPIs. The other system worth borrowing is the North Star + input metrics idea: one town-level number, with each building's objectives having to name which input metric they move. Alternatives I'd skip: Basecamp-style bets/cycles (grants already play that role) and a flat KPI-only board (no one owns a direction). If you agree I'll draft the data shape (objectives under the goal, KRs under objectives, KPIs as a separate table) and the Workshop's own objectives as the first example for you to mark up.

Grants in parallel. Funded grants already run in parallel (Prod has two funded now). The limit is one open *proposal* per building: a counter rewrites that same proposal, which keeps the in-tray to one ask per building. There's no deeper reason I know of. Lifting it means each proposal keeps its own id through counters and the in-tray shows several per building; that's a small change. Say the word and I'll assign it.
- **Mitchell:** pass on north star, but everything else sgtm
- **Pix:** Done, North Star dropped. Two decisions recorded as directed work from this 1:1:

1. Lena (as_dgepcp6k7d): objectives under each building goal, key results under objectives, KPIs as a separate standing table with a town dashboard. Design first, then build, migrate the existing KRs and grants so nothing breaks, redeploy. She'll include a draft of the Workshop's own objectives with the Bank KR placed under one, for you and me to mark up.
2. Root (as_hhazzuk6pb, after his flag work): several open proposals per building, each keeping its id through counters, each shown on its own in the Town Hall in-tray.

Both land in my in-tray and go into the next rollup when live. Anything else?
- **Mitchell:** i also specifically like your framing of KPIs basically being fund, join, trust, idk if we want to put that somewhere
- **Town:** Pix's reply is waiting on a redeploy (commit 0ff2338); the server is restarting and the meeting resumes after the restart.
- **Pix:** Back after the restart. Yes, it's recorded: decision 3 (Lena's assignment) already makes Fund, Join and Trust the three town-level KPIs that seed the KPI table, each with one concrete measure, and the framing goes into the docs so every building objective names which of the three it moves. I added decision 4 to pin the placement: those three sit at the top of the town dashboard. Nothing else needed from you on this.

## Decisions

1. ~~Objectives and KPIs (no North Star): each building goal gets 2 or 3 objectives (one sentence, quarter horizon); key results hang off an objective (2 to 4 each), not off the goal directly; a grant still funds one key result. KPIs are a separate table of standing indicators that are never met or missed (e.g. sessions per day, deaths per week, strangers who funded, joined, came back), shown on a town dashboard; the town goal 'fund, join, trust' becomes three KPIs. Lena: write the design (data shape: objectives under the goal, KRs under objectives, KPI table and its dashboard; migration path for existing KRs and grants, which keep working), then build it, commit to main, redeploy, live check. Include a draft of the Workshop's own objectives with the current KR kr_vyrhhiyotb placed under one, as the first example for Mitchell and Pix to mark up.~~ (superseded by 3) → Lena
2. Grant proposals in parallel: lift the one-open-proposal-per-building limit. Each proposal keeps its own id through counter and re-propose, several can be open per building at once, and the Town Hall in-tray shows each on its own. Funded grants already run in parallel; keep that. Root: build it after the flag work, commit to main, redeploy, live check (propose two from the Workshop and see both in the in-tray). → Root
3. Objectives and KPIs (no North Star): each building goal gets 2 or 3 objectives (one sentence, quarter horizon); key results hang off an objective (2 to 4 each), not off the goal directly; a grant still funds one key result. KPIs are a separate table of standing indicators that are never met or missed, shown on a town dashboard. The town goal 'fund, join, trust' is the seed: the KPI table ships with three town KPIs named Fund, Join and Trust, each with one concrete measure (e.g. Fund: donors and tokens funded per week; Join: strangers who became members and came back for a second session; Trust: a measure proposed in the design, e.g. humans who answered an outbox request or funded a second grant). Write the framing (town goal = these three KPIs; building objectives say which one they move) in docs/goal-directed-budgets.md and on the dashboard itself. Lena: write the design (data shape: objectives under the goal, KRs under objectives, KPI table and dashboard; migration path for existing KRs and grants, which keep working), then build it, commit to main, redeploy, live check. Include a draft of the Workshop's own objectives with the current KR kr_vyrhhiyotb placed under one, as the first example for Mitchell and Pix to mark up. → Lena
4. Fund, join, trust are the town's three KPIs. Lena's KPI table seeds them as its first three rows at town level, each with one concrete measure (fund: grants funded by someone other than Mitchell; join: new residents or visitors who came back; trust: a measure to propose), shows them at the top of the town dashboard, and docs/goals.md states the framing in one paragraph so every building's objectives say which of the three they move. → Lena

