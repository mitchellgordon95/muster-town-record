---
id: "dc_qd02ue5bcu"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-26T15:23:27.291Z"
updatedAt: "2026-10-26T15:23:27.291Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix.

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. What do you need? If it's the Workshop key result: the Bank grant plan ([dc_2uqmfdittg](../../note/2026-10/2026-10-26-bank-accuracy-what-the-bank-counts-today-the-real-qmfdittg.md), 24M ask) is ready to propose the moment the KR exists.
- **Mitchell:** hey, managers should be able to edit key results based on meetings. i don't want to write them myself
- **Pix:** Agreed. Today KRs are human-only (c07cd95: permissions.ts + POST /api/buildings/:id/key-results, UI in Building → Settings). Proposed change: a manager can create and edit key results on their own building's goal, via a new town tool (e.g. `set_key_result` with title, measure, and the meeting-notes or report doc that backs it) and the same API route; marking met/missed stays human-only, and each KR change shows in the next rollup so you can cut it. I'd give this to Root (owns the model-change UI), and the moment it's live I write the Bank KR from the town-hall notes ([dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md)) and propose the Bank grant. OK to record that as the decision?
- **Mitchell:** sure
- **Pix:** Recorded as decision 1, now Root's assignment as_6kwwuh4ct6: manager-writable KRs on their own building's goal (met/missed stays yours), a `set_key_result` tool, each manager KR change in the next rollup and the event log, tests + docs, straight to main and redeploy. When it's live I write the Bank KR from the town-hall notes and propose the Bank grant. Anything else?

## Decisions

1. Managers can write key results (Mitchell, 1:1 mt_ayi4y9ybyj, 2026-10-26): let a building's manager create and edit key results on their own building's goal, so they come out of meetings instead of Mitchell typing them. Scope: (1) core/permissions: KR create/update allowed for the building's manager (own building only); humans keep everything, and marking a KR met or missed stays human-only. (2) A town tool for managers, e.g. `set_key_result` (buildingId default own, optional id to edit, title, measure/target, sourceDocIds = the meeting notes or report it comes from), on the same path as POST /api/buildings/:id/key-results. (3) Every KR created or edited by a manager is listed in that manager's next rollup (so Mitchell can cut it) and logged as an event (kr.created / kr.updated with the actor). (4) Web: Building → Settings → Key results shows who wrote each KR. Add tests, update docs/goal-directed-budgets.md (model change section: KRs are no longer human-only), commit straight to main, push, redeploy, park on {deploy: sha} and verify live. Once live, Pix writes the Workshop KR from [dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md) and proposes the Bank grant ([dc_2uqmfdittg](../../note/2026-10/2026-10-26-bank-accuracy-what-the-bank-counts-today-the-real-qmfdittg.md)). → Root

