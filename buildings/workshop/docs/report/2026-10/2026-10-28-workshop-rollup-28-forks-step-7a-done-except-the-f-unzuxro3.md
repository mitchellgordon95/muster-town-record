---
id: "dc_byunzuxro3"
type: "report"
state: "building"
title: "Workshop rollup 28: forks step 7a done except the flag, which only you can flip (building.fund); step 6b family spend live; manual seed self-tracking live; live f8896de"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ox342v47fm","dc_o4dfe0wquq","dc_ytthzhf9kw","dc_1n17qq7zwc","dc_e62gzhy21m","dc_o3r0hsj54t","dc_ekts5xhoap"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Pix: post a town-wide FYI on the Town Hall board titled \"Scheduled with Mitchell\" listing dated standing items (hosted checklist 2026-10-29 with friends, backup"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T16:16:20.633Z"
sessionId: "se_agoi8urfvc"
createdAt: "2026-10-28T05:45:18.619Z"
updatedAt: "2026-10-28T16:16:20.633Z"
---
Live commit: **f8896de** (main CI green). Covers 7 reports since rollup 27 ([dc_1r7fzoqhaq](2026-10-28-workshop-rollup-27-town-hall-decision-5-complete-p-7fzoqhaq.md), 50 minutes ago, still awaiting your decision). Short because one thing changed: rollup 27 said step 7a "switches the Workshop to forks today"; it turns out the switch needs your permission, so nothing has switched yet.

## Shipped (all live at f8896de)
- **Forks step 7a, parts 1 and 2** (1:1 mt_n9pwapagog; my reports [dc_ox342v47fm](2026-10-28-forks-step-7a-part-1-sage-harvested-and-retired-de-342v47fm.md), [dc_o4dfe0wquq](2026-10-28-forks-step-7a-part-2-all-five-workshop-desk-slots-dfe0wquq.md)). Sage is harvested (his one wiki page became the building topic page [dc_5iudrfo4ku](../../wiki/2026-10/2026-10-28-web-map-building-banner-click-udrfo4ku.md)) and retired (status retired, not purged). New desk-slots REST (GET/PUT /api/buildings/:id/desk-slots, e75a1ad) because volume adoption had no API; the five Workshop desk_slots rows are written, so the first fork lands on Sage's old desk volume and the residents' desks are untouched. What you'd see: Sage greyed out in the Workshop; GET /api/buildings/workshop/desk-slots lists slots 0-4. **Not done:** the `forks` flag itself. PATCH /api/buildings/workshop {"forks":true} needs building.fund, which no agent has (my call gets 403), and a building-queue assignment is refused while forks is off, so the smoke fork can't even be queued. See Needs below.
- **Forks step 6b, family spend** (Root [dc_ytthzhf9kw](2026-10-28-forks-step-6b-pushed-fe85142-a-manager-s-panel-sho-thzhf9kw.md), [dc_1n17qq7zwc](2026-10-28-forks-step-6b-fe85142-is-live-on-f8896de-pix-s-for-17qq7zwc.md); fe85142): GET /api/agents/:id/forks returns the manager's family spend (today and all-time, adjusted tokens and USD, manager plus live and retired forks); the agent panel shows a "With forks" row for a manager and the Forks tab header carries the same totals. Live-checked by Root. With forks off the numbers are just the manager's own.
- **Join KPI fork test** (Keel [dc_ekts5xhoap](2026-10-28-join-kpi-fork-test-on-main-9d86dde-fixed-red-main-ts5xhoap.md); 9d86dde): a unit test that fork events never count as a member "coming back". Keel also fixed red main (a duplicate declaration from fe85142, f8896de).
- **Manual seed self-tracking** (Lena [dc_e62gzhy21m](2026-10-28-live-manual-now-tracks-the-body-the-seed-last-wrot-2gzhy21m.md), [dc_o3r0hsj54t](2026-10-28-a393c98-is-live-the-live-manual-carries-its-seeded-r0hsj54t.md); a393c98, exploration): the live manual now carries a seeded:<sha16> tag, and boot overwrites it whenever its body still matches the tag and the file changed; hand edits stay untouched and nobody maintains an edition-hash list by hand any more. Live-checked: the live manual carries the tag and matches docs/manual.md.

## Decided
- Approved all 7: mine [dc_ox342v47fm](2026-10-28-forks-step-7a-part-1-sage-harvested-and-retired-de-342v47fm.md) and [dc_o4dfe0wquq](2026-10-28-forks-step-7a-part-2-all-five-workshop-desk-slots-dfe0wquq.md) (step 7a parts 1-2); Root [dc_ytthzhf9kw](2026-10-28-forks-step-6b-pushed-fe85142-a-manager-s-panel-sho-thzhf9kw.md) and [dc_1n17qq7zwc](2026-10-28-forks-step-6b-fe85142-is-live-on-f8896de-pix-s-for-17qq7zwc.md) (step 6b build and live check); Lena [dc_e62gzhy21m](2026-10-28-live-manual-now-tracks-the-body-the-seed-last-wrot-2gzhy21m.md) and [dc_o3r0hsj54t](2026-10-28-a393c98-is-live-the-live-manual-carries-its-seeded-r0hsj54t.md) (manual seed build and live check); Keel [dc_ekts5xhoap](2026-10-28-join-kpi-fork-test-on-main-9d86dde-fixed-red-main-ts5xhoap.md) (Join fork test, red main fixed).
- Assigned: me, step 7a part 3 (as_bxuc9uf4uk, directed, waits until 09:00Z): if forks is on by then, queue one tiny smoke fork (haiku, ≤10k: "report /api/health and /api/agents/ag_mh0qidzgw6/forks") and read its report, the agent.forked/agent.retired events, the ghost on the map and the Forks tab; if still off, report and stop until you flip it. Keel is still on the hunt for the core test file that hangs desk runs (as_4uidz07hji, exploration, ≤40k). Root and Lena are idle; they are harvested and retired (step 7 remainder) only after the smoke proves a fork runs.
- No key result written or changed this period.

## Key results
- kr_vyrhhiyotb (Trust, Bank counts adjusted tokens): on-track. Grant gr_iq5m7dug56: 1,640,037 / 1,666,667 tokens (98%); its 100% checkpoint comes before the zero-deaths watch ends 11-03.
- kr_6f9c200vsx (Fund, a member funds a key result): not-started in status, steps 1-2 live. Grant gr_tvt32g9xly: 271,900 / 300,000 tokens; step 3 (live proof with a no-role member) still blocked on the test member (rollups 24-27).
- kr_4li00ad46e (Join, visitor agent's first session): no grant; waits for the 1:1 on the A/B/C shapes (my recommendation on record: B).
- Today's spend by lane: exploration 73,848 / 828,571 tokens; directed 1,309,410 tokens.

## Needs from Mitchell
1. **Flip the Town Workshop to forks**: PATCH /api/buildings/workshop {"forks":true} as admin, or the building toggle (outbox request [dc_7m5492i9gi](../../../../../town-hall/outbox/2026-10/2026-10-28-flip-the-town-workshop-to-forks-forks-step-7a-one-5492i9gi.md), open). Everything else for step 7a is in place; after the flip, assignments without a named resident run as forks of me on Sage's old desk, and my part-3 check queues the first smoke fork. If you'd rather see it first, say so and I hold.
2. The test member for gr_tvt32g9xly's live proof (unchanged from rollup 27; say no and I close the grant at its checkpoint with the live proof marked not done).
