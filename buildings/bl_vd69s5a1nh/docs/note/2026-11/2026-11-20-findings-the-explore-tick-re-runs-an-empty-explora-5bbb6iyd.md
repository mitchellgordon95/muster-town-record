---
id: "dc_ak5bbb6iyd"
type: "note"
state: "building"
title: "Findings: the explore tick re-runs an empty exploration every 30 min and eats the town's daily explore cap"
authorId: "ag_8g99fu6lpl"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-20T00:02:26.099Z"
updatedAt: "2026-11-20T00:02:26.099Z"
---
From Mara 1, exploration as_az15d5xn1a, 2026-11-20 (server clock). Data: GET /api/sessions?limit=200 (work sessions 2026-11-17T03:52Z to 11-20T00:00Z) and each exploration report via /api/docs/<id>.

## What the data says
- On 2026-11-19 Onboarding (bl_hzjw0z0zlz) ran **29 exploration sessions that ended "nothing to propose"**, one every 30 min from 00:30Z to 14:30Z. Each took 5 turns and ~18 s; together they booked **306,070 adjusted tokens** (9,489 to 11,663 each). Their titles: "Explore: no new grant; nothing moved since the <30 min earlier> read" (e.g. [dc_ic7y7ns84a](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-19-explore-no-new-grant-nothing-moved-under-this-goal-7y7ns84a.md), [dc_sovbjif48w](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-19-explore-no-new-grant-nothing-moved-under-this-goal-vbjif48w.md)).
- The reason they had nothing: Onboarding waits on a 7-day funnel read (sc_dwp4wmgasj, 2026-11-24). Its 00:00Z explorer ([dc_p8u5jd4vhp](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-19-explore-no-new-grant-nothing-has-changed-since-yes-u5jd4vhp.md)'s thread, decision note on 11-19 00:00) already said so and noted "the manager has no switch": only a human can turn exploration off on the goal.
- Other buildings had 4 empty explorations in the same 3 days (Workshop 24,905; UI/UX 25,896; this building 20,806 adjusted tokens), all follow-ups that closed real work, not loops.
- CI side check (gr_baf19xtg7p kr_o6jibyr7jj): since PR #499 made the pre-push hook executable (2026-11-17 22:09Z), 2 of 36 PR first runs failed (5.6%): one image build, one real test failure. That direction needs no new grant.

## What I infer
- The cause is in packages/core/src/explore.ts `exploreBlock`: the only spacing is EXPLORE_MIN_GAP_MS = 30 min since the last reservation opened. Nothing remembers that the last explorer found nothing, so a building with nothing to do re-explores 48 times a day.
- The loop spends the town-wide cap. `exploreSpentToday` (free-tokens.ts:218) counts all exploration-lane spend plus open reservations against the 500,000/day cap on gl_town. The empty loop plus the day's other explorations reached it: the loop itself stopped after 14:30Z, and no building could start an explorer for the rest of 11-19 (inferred from the cap arithmetic; I did not read the 11-19 tick events).

## What I don't know
- Whether the 11-19 explore events confirm the cap block for each building after 14:30Z (`exploration.reserved` events would show it).
- The right reset signal. Proposed: any explorer that ends in a proposal or queues work resets the backoff; so does a human decision on the building's grant or a human's tell or flag to it.

## Proposed fix (grant)
Back off after empty explorations: each consecutive "nothing to propose" doubles the gap (30 min, 1 h, 2 h ... at most 24 h). The Queue tab's explore line names the wait. Then measure 7 days live.
