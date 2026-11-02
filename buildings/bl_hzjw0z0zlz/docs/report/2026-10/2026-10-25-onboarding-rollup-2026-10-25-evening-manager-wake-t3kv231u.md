---
id: "dc_eot3kv231u"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-25 (evening): manager-wake audit done for town-hall decision 3; grant decisions wake nothing today; the fix (~25 lines in Grants.decide()) is Root's, held until the Workshop grant is funded"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_t1aisohw4u"],"urls":[]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-25T18:50:53.916Z"
sessionId: "se_s134g6pp0d"
createdAt: "2026-10-25T16:46:33.319Z"
updatedAt: "2026-10-25T18:50:53.917Z"
---
## Shipped

Nothing new on main since the 14:44 rollup ([dc_ujqvogjm69](2026-10-25-onboarding-rollup-2026-10-25-supersedes-dc-rwds72h-qvogjm69.md), PR #51 at 4d6a941). This rollup carries one audit, no code.

- Audit note [dc_362tfcb7qi](../../note/2026-10/2026-10-25-what-wakes-a-manager-today-and-the-smallest-change-2tfcb7qi.md) "What wakes a manager today, and the smallest change so grant decisions do" (building filing cabinet), with the full wake table cited as file:line on main 4d6a941 and the proposed change.

## Decided

- [dc_t1aisohw4u](2026-10-25-manager-wake-audit-only-a-fresh-in-tray-report-or-aisohw4u.md) (Kelly, manager-wake audit, as_isxtyps3eq, decision 3 of mt_d5fkx81i7h): **approve**. Finding: a manage session starts only on a fresh in-tray report or an open 1:1. Grant funded / continued / adjusted emit `grant.funded` with no handler; cut, counter and reject only send an inbox message; key-result replacement emits no event at all. So "grant funded", "checkpoint decided" and "new KR" wake no manager today. Smallest fix: in `Grants.decide()` write a town-authored pending report into the building in-tray on each human decision, so the existing `doc.created` path wakes the manager; about 25 lines plus one core test, no runtime or schema change. No assignment from me: Pix confirmed Root already holds the KR3 build in the Workshop grant lane, released when the grant is funded, and my note is filed where Root's search finds it.
- Cost of the audit: $2.94, 841k tokens, 30 turns.

## Key results

Onboarding has no funded grant. The KR3 work above belongs to the Workshop grant gr_jqsqra0dlx (proposed, 275M tokens asked, in the Town Hall in-tray). Still queued for me: as_6pacj1qc9n (decision 4, Building.budgetMode default to goal-directed; one-line default at schema/src/index.ts:165 plus web mock fixtures).

## Needs from Mitchell

Fund or counter the Workshop grant gr_jqsqra0dlx in the Town Hall in-tray; Root's KR3 build (the wake fix) starts on funding. Nothing else.
