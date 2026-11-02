---
id: "dc_9pz8e24o41"
type: "report"
state: "building"
title: "Design doc docs/goals.md ready for Mitchell: one town-level goal tree (draft PR #116)"
authorId: "ag_1iw7qgvvut"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_a3nvwfawer","dc_0xqyrevla1","dc_72nexb0bwn","dc_oghes5lgud"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/116"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Design doc docs/goals.md as draft PR #116 (Pix 2), per 1:1 mt_a3nvwfawer decision 1. Design only, no code. Mitchell told in the 1:1; the build waits for his read and his answers to the 5 open questions. Rollup 31 Shipped candidate (API/doc-only item, no picture)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T18:15:01.218Z"
sessionId: "se_0grabjfs14"
assignmentId: "as_s5zqdgk3zi"
costUsd: 1.227515
tokens: 61376
turns: 25
createdAt: "2026-10-30T18:14:51.849Z"
updatedAt: "2026-10-30T18:15:01.218Z"
---
## What I did
I rewrote the 3-line `docs/goals.md` stub as the design doc Mitchell asked for in 1:1 mt_a3nvwfawer (about 3,100 words, roughly a 12-minute read). It is a draft PR: https://github.com/mitchellgordon95/muster-town/pull/116 (commit on branch agent/pix-2/design-doc-docs-goals-md-town-level-goal). It is design only, with no code and no redeploy. The migration section uses the code (grants.ts, lanes.ts, migrations 025/032/043) and the live town at commit 02f1bbe. The docs reference check passes. Topic page: [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md).

## Findings
What the doc says:
- **Model.** There is one town tree. The root goal sits above three goals, Fund, Join and Trust, each watching its KPI dial. Below them are **standing goals**: never met, and only a human retires one. **Key results** are the leaves. Each is dated and is either a target on a dial by a date or a concrete thing in the live town. A KR that is met or missed archives under its goal, and the goal stays. KPI dials are computed live in `kpis.ts`; they are not nodes.
- **The KR test.** A fork can propose a grant against it without asking anyone, and a human can check it in the live town.
- **New tables.** `goals`, `building_goals` (a building attaches to one or more subtrees) and `goal_proposals`. `key_results` gains `goalId`, `due`, `kpiId`, `target` and `archivedAt`.
- **Grants.** They keep `keyResultId`. Only the scope check changes: from "the KR belongs to my building" to "an open KR in my subtree". This is one helper, used in `grants.ts` and `lanes.ts`. History comes from the event log, with who and when on every edit.
- **Who edits.** Humans with a new `goals.edit` permission edit the tree. Managers and their forks only propose: `set_key_result` and `set_objective` become `propose_goal` and `propose_key_result`.
- **Town Hall editor.** It has three parts: the tree (status, due date, dial reading, grant word and attached-building chips on each row), node detail with a History tab, and a proposals strip with Accept, Edit and accept, and Cut. Goal proposals also show up in the in-tray and the review deck.
- **Lanes.** Grant lanes are unchanged. Exploration and directed work name a KR inside the building's subtree. The exploration allowance stays per building. A building is blocked when it has no attachment, or when its subtree has no open KR and no funded grant; in that case its manager is woken to *propose* the next KR.
- **Planner.** A Town Hall resident that opens from "Plan with an agent". It starts loaded with the tree, the dials, an event-log digest, the latest rollups and open proposals. It drafts proposal cards inside the 1:1 and never edits the tree itself. Its first jobs: promote the met KRs that were really standing goals, put dates on migrated KRs, and give each KPI one dial-target KR.
- **Cadence.** No scheduled meetings. Everything queues for the morning and evening review. Each human gets their own "since your last review" marker, and the first deck slide shows edits by other humans. Meetings are for three things only: planning when the tree changes materially, ordinary 1:1s, and the Planner 1:1.
- **Removed.** Goal editing on the planning map, which keeps one "Attached to" line. The building Goals tab becomes a read-only view of the building's subtree plus a "Propose a key result" form. Objectives become goals, and `set_objective` goes away. Grants, checkpoints, the Bank and the lanes gate are untouched.
- **Migration.** One additive migration. Its number gets checked against main at merge time; it would be 061 today. Each objective becomes a goal with the same `ob_` id, under its KPI goal. KRs without an objective go under a new `gl_<buildingId>` goal per building. Met and missed KRs are archived. Grants are not touched. Live counts: 14 goals, 31 KRs keeping their ids and statuses (19 open, 12 archived), and 27 grants unchanged, 4 of them funded (gr_iq5m7dug56, gr_tvt32g9xly, gr_rntk0echpi, gr_8cdix9mpye). Two buildings come out blocked: Bank Transparency (all its KRs are met) and UI / UX (no goals to attach).
- **Build order:** 5 steps, listed in the doc.

Open questions in the doc:
1. Who pays for Planner?
2. Should a KR whose dial crosses its target be set to claimed automatically?
3. What happens when someone retires a goal that still has open work?
4. Must every goal sit under Fund, Join or Trust?
5. Should a new building start unattached?

## What I need from you
Mitchell: read PR #116 (docs/goals.md) and answer its 5 open questions before anyone starts the build.
