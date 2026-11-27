---
id: "dc_066ku9sigj"
type: "report"
state: "building"
title: "Explore backoff 7 days: 6 empty explorations (was 30 in a day); one day over 100k empty tokens, before Onboarding's cap"
authorId: "ag_r0dtnxolwy"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 3 read taken in: backoff and journal both work; kr_vlloruojvk fails on 11-22 only (157,526 empty tokens, before Onboarding's cap). Since only a human marks a key result missed, the gate card on gr_6id9g7u9cj carries it: Cut recommended, nothing left to run. No work queued."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-27T06:05:22.518Z"
sessionId: "se_5isvsxdxwi"
assignmentId: "as_6zh0b7m37z"
costUsd: 1.8979243000000001
tokens: 94896
turns: 30
createdAt: "2026-11-27T06:03:45.859Z"
updatedAt: "2026-11-27T06:05:22.518Z"
---
## What I did
Read every exploration that started between 2026-11-20 03:00Z and 11-27 03:00Z. I used the `exploration.*` events from /api/events, and each explorer's sessions from /api/sessions?agentId=… (that endpoint returns at most 200 rows and has no offset). I also read the live queue of all 7 buildings and all 7 "Exploration journal" pages. I changed no code. Topic page [dc_3fzkzkox1e](../../wiki/2026-11/2026-11-20-explore-backoff-and-journal-zkzkox1e.md) is rewritten with these numbers.

## Findings
**Volume.** 31 explorations cost 2,088,323 adjusted tokens. 25 filed a proposal. 6 were empty (verdict stop, no proposal), all at Onboarding, for 181,611 tokens. For comparison, Onboarding ran 30 empty explorations on 11-19 alone.

| UTC day | explorations | tokens | empty | empty tokens |
|---|---|---|---|---|
| 11-21 | 6 | 428,087 | 0 | 0 |
| 11-22 | 9 | 427,648 | 5 (Onboarding) | **157,526** |
| 11-23 | 5 | 357,275 | 0 | 0 |
| 11-24 | 6 | 450,827 | 1 (Onboarding) | 24,085 |
| 11-25 | 4 | 325,346 | 0 | 0 |
| 11-26 | 1 | 99,140 | 0 | 0 |
| 11-20 (from 03:00) and 11-27 (to 03:00) | 0 | 0 | 0 | 0 |

- **kr_vlloruojvk (empty-exploration tokens under 100,000 every day): fails on 11-22 only.** 6 of 7 days pass.
  - On 11-22, Onboarding's runs started at 00:01, 01:00, 03:00, 07:00 and 15:00. Each found nothing and cost 13.5k–47k tokens: [dc_hgeg5eovv6](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-22-explore-no-new-grant-blog-readers-skip-the-homepag-eg5eovv6.md), [dc_i48s358mol](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-22-explore-no-new-grant-nothing-moved-since-the-00-01-8s358mol.md), [dc_xzpflqumsh](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-22-explore-no-new-grant-nothing-moved-since-the-01-00-pflqumsh.md), [dc_9vnfqhu0lq](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-22-explore-no-new-grant-nothing-moved-since-the-03-00-nfqhu0lq.md), [dc_vtct8q8m3i](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-22-explore-no-new-grant-nothing-moved-since-the-07-00-ct8q8m3i.md).
  - The 1h/2h/4h/8h gaps show the backoff working. But Onboarding's own work on 11-20 and 11-21 had reset its streak, and five doublings fit inside one day.
  - Onboarding's 100k/day exploration cap was only set at 11-22 18:19Z, after all five runs (Kelly's ask "Save the 0.1 million a day exploration cap", which Mitchell decided).
  - Since PR #598 (11-24), the cap comes from desks: Onboarding's is now 68,181 a day. No day has gone over since then.
  - Smallest fix if the KR must hold strictly: none is needed for a single building, because the cap now limits it. Nothing in the code limits the town-wide total of empty explorations. I am not proposing that work.
- **kr_aael00nhjw (no building over 6 empty explorations a day, and the backoff line shows): claimed.**
  - The highest count was 5 in a day (Onboarding, 11-22).
  - The backoff line was seen live on 11-20 at 02:38Z (step 1).
  - At 06:02Z today, all 7 queues (GET /api/buildings/<id>/queue) say "a proposal of this building is open and undecided" instead. That block takes priority, so no backoff line is showing right now.
- **kr_e5l200kv9z (one journal line per exploration, and reports name the lines they read): claimed, with one exception.**
  - All 31 explorations have a town-written line on their building's page: [dc_o9ohlvrmii](../../wiki/2026-11/2026-11-20-exploration-journal-ohlvrmii.md), [dc_q1hxxxuwzs](../../../../bl_vef3v0oux0/docs/wiki/2026-11/2026-11-20-exploration-journal-hxxxuwzs.md), [dc_dt4yaul98t](../../../../bl_xvgnd1fvh6/docs/wiki/2026-11/2026-11-20-exploration-journal-4yaul98t.md), [dc_7ibmbmvafb](../../../../bl_6ifesdbah3/docs/wiki/2026-11/2026-11-20-exploration-journal-bmbmvafb.md), [dc_ki0mb83ywu](../../../../workshop/docs/wiki/2026-11/2026-11-20-exploration-journal-0mb83ywu.md), [dc_sykhvvd4un](../../../../bl_t7slw19vgg/docs/wiki/2026-11/2026-11-20-exploration-journal-khvvd4un.md), [dc_uxt4oy6xjf](../../../../bl_hzjw0z0zlz/docs/wiki/2026-11/2026-11-20-exploration-journal-t4oy6xjf.md).
  - 30 of the 31 reports name the lines they built on or say none applied. One example is dc_yr4wjadf3z: "none of its lines apply".
  - The one report that does not is [dc_2mj02mm58z](2026-11-22-proposed-gr-3h504nqqdp-desk-sessions-survive-an-un-j02mm58z.md). That run had to start over after the restart at 11-22 18:29Z cut it short, and its report does not mention the journal.
- **Side gap, still open.** A reservation's `spentTokens` is still booked as 0 or too low when the session ends after the reservation closes. All 6 empty Onboarding runs booked 0. The journal and the daily cap read the sessions instead, so their figures are right.

The backoff and the journal both work. One KR missed on one day, before Onboarding's cap existed. That is the manager's call: close_grant with kr_vlloruojvk marked missed, or as the human decides.

## What I need from you
Decide whether to close gr_6id9g7u9cj with kr_vlloruojvk marked missed (11-22: 157,526 empty-exploration tokens).
