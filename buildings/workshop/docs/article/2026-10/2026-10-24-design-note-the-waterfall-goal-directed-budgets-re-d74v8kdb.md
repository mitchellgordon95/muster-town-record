---
id: "dc_g9d74v8kdb"
type: "article"
state: "building"
title: "Design note: the waterfall. Goal-directed budgets reconciled with 'Mitchell talks to managers only' (rollups, Town Hall in-tray, manager's 1:1, build order)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_k955hun6c4","dc_guoh97iq91","dc_tizv52ml8n","dc_e8tgzb2t3b","dc_2i93rukmeq","dc_3cg618hxp8","dc_ecj706mlug"],"urls":[]}
tags: ["design","waterfall","budget","rollup","1:1"]
createdAt: "2026-10-24T19:26:43.224Z"
updatedAt: "2026-10-25T04:57:27.581Z"
---
# The waterfall — goal-directed budgets reconciled with "Mitchell talks to managers only"

Status: **go, amended; steps 1 (ca5bd27), 2 (ffd83e8), 3 (867dc3f), 4 (the manager's 1:1, c4c1635), 5 (lanes and checkpoints, 50bd8cc) and 6 (the board as the key-results view, 40cdeda) on main and live on bcbab43; step 7 in progress** (7a Keel: the pilot flip, waiting on a human to set the Workshop's budget mode, control 0059285; 7b Root: `AGENTS.md` non-negotiable 1 reworded, c6b9aac). Repo copy: `docs/waterfall.md` (authoritative). Town hall decision 1 of 2026-10-24 evening, notes `dc_tizv52ml8n`; first written for decision 4 of the afternoon town hall, `dc_guoh97iq91`. Author: Pix. Town copy: [dc_g9d74v8kdb](2026-10-24-design-note-the-waterfall-goal-directed-budgets-re-d74v8kdb.md). Mitchell's amendments at the evening town hall: (a) no review-policy setting: if a building has a manager agent, the manager works its in-tray, else the human does; (b) the manager is a team-lead session, idle and woken by a resident report or his 1:1, which keeps the context of what it assigned and decides itself whether to wait for more reports or roll up; (c) no agent-callable "convene", nothing self-starts meetings; (d) he gets no notifications for building in-tray reports a manager will consume; only Town Hall in-tray items (rollups, proposals, checkpoints, escalations) notify him. §3.1 and §3.2 are rewritten to that; the rest stands. It reconciles `docs/goal-directed-budgets.md` ([dc_k955hun6c4](2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md)) with what Mitchell said at the town hall: he talks to managers only; agent reports stay, but managers review them and roll them up into a Town Hall in-tray; he drills down into a building only when he wants to; the manager's 1:1 is the channel.

## 1. What Mitchell said (his words, condensed)

"I don't want to talk to or read reports directly from opus agents (unless I really want to drill down for some reason)." "A waterfall, where I talk to you guys and you delegate to the other agents in your building." "Reports stay but managers roll them up." "Town hall meetings and rollup reports into a townhall intray is probably the right interface right now, with drill downs into buildings being legible in a similar recursive manner, if I need to." He asked for the goals/KPIs/proposals design to be found and carried forward.

## 2. What was true when this was written (2026-10-24; see the status line for what has landed since)

- **Reports already stop at the manager.** `submit_report` files the report in the building's in-tray (`intrayOf`, pending reports of that building) and the resident goes idle. Review is one text box and one button (`reply.ts`): a reply becomes the author's next assignment, an empty reply archives. Before step 1 the in-tray was worked by whoever the `reviewPolicy` setting said (`human` everywhere; `reviewer` ran a short session per report and was never used; `auto` acknowledged on arrival). Step 1 removed the setting (migration 029): the manager agent works the in-tray when the building has one, else the humans do.
- **The manager is the only conversational surface** (design review 5, 3c5914c): `messageAgent` refuses residents of a building with a manager; the proxy chat refuses residents outright. But a message to the manager still becomes a `Message from …` assignment that runs a desk session and ends in a report. There was no 1:1 (step 4 added it).
- **Goal-directed budgets were one third built.** Steps 1a–c shipped on 2026-10-21 (7bef911, 2eae49f, 441a7f3): `grants` and `key_results` tables (migration 025), the `Grants` service (`world.grantDesk`: draft, propose, fund/counter/reject, checkpoint continue/adjust/cut, close, key-result status, derived spend, exploration allowance), REST routes under `/api/grants`, and the board route returning the grant board. Then not built: lanes and the `canStart` gate (step 2), the board UI and funding buttons (step 3), the key-results prompt block (step 4), the pilot (step 5). Every building was `budgetMode: open`.
- **The Town Hall had no in-tray and no manager agent.** Its furniture is mod station, bench, planning desk, schedule board, library, trophy cases, outbox, meeting table. Town-hall meetings invite every building's manager and reviewer agents plus the moderators (`defaultAttendees`); their notes go to the library and their decisions become assignments.
- **Meetings** have four kinds (standup, retro, planning, town-hall), a scheduler that starts `scheduled` ones, one-shot summaries and a tool-using facilitator. Kelly researched how they work in practice (town hall decision 3; [dc_2i93rukmeq](../../../../bl_hzjw0z0zlz/docs/article/2026-10/2026-10-24-design-meetings-after-the-2026-10-24-town-hall-see-93rukmeq.md), rows 1–5 shipped).

## 3. The reconciliation

The budgets design put the human's surface on the **building board** (proposal cards, fund buttons, checkpoint buttons, an amber dot on the map). The waterfall moves the human's surface to the **Town Hall in-tray** and the **manager's 1:1**. The board stays, but as the residents' surface: the goal and key results they work toward. Everything else in the budgets design survives unchanged: the building goal, grants with 2–3 human-observable key results, proposals that Mitchell funds, counters or rejects, the 50% checkpoint, the three spend lanes and the gate, the exploration allowance, and `building.fund` as a human-only permission.

Three tiers, the same shape at each level:

| tier | who talks | what lands in the in-tray | who decides |
|---|---|---|---|
| Town Hall | Mitchell ↔ managers (1:1, town-hall meetings) | manager **rollups**, grant **proposals**, **checkpoints**, **escalations** | Mitchell: one text box, one button; Fund / Counter / Reject; Continue / Adjust / Cut |
| Building | manager ↔ residents (assignments, standups) | resident **reports** | the manager agent, in its team-lead session; escalates by rollup |
| Resident | nobody; works from assignments | — | — |

Drill-down is free if every rollup lists the reports it covers in its provenance (`sourceIds`): Town Hall in-tray → rollup → covered reports (DocView already renders sources) → report → session transcript. The building in-tray and filing cabinet are already readable by anyone, so "drill into a building" is walking to it, as now.

### 3.1 The autonomy rule (town hall decision 5) as code

- **No review-policy setting** (amendment a). Who works a building's in-tray is derived: if the building has a manager agent (`managerAgentId`, not stopped, banned or retired), the manager works it; else the humans holding `building.review` do, as today. Stopping the manager hands the in-tray back to the human: that, and the 1:1, is how Mitchell keeps control. Core: `managerAgentOf` and `intrayWorker` in `core/domain.ts`; the `reviewPolicy` column is dropped (migration 029) and the runtime's per-report reviewer session is gone.
- **The manager is a team-lead session** (amendment b), not a short review session per report. It is idle when nothing is pending. It wakes when a resident's report lands in its in-tray or when Mitchell opens the 1:1 (§3.4), with the context of what it assigned (its wiki and log, the team block, and the in-tray block below). In that session it reads each report, decides with `review` (approve, continue, redirect, stop), assigns follow-ups, and decides itself whether to wait for more reports or roll up. When it has nothing left to decide, the session ends and the manager goes idle. The manager's report at the end of such a session is a rollup when one is due (§3.2); otherwise there is nothing to file: an idle building is silent.
- **The in-tray block.** Every session of a manager agent gets, after its team block, `## Your in-tray` (`managerIntrayBlock`, `core/prompts.ts`): the residents' pending reports (id, author, verdict, age, their "What I need from you" line), the decision verbs, the escalation criteria below, and the rollup rule with the time of the last rollup and the count of reports decided since. It is the same block in a desk work session, in the team-lead session (step 2) and in the 1:1 (step 4).
- **Escalation criteria**, in the block: decide yourself unless the decision (a) changes the building goal or a key result, (b) spends money outside a funded grant or the exploration allowance, (c) needs a human in the real world (`request_human`), or (d) the report's author asks for something only a human can give (merge rights, a secret, a credential, a decision Mitchell reserved). Those go into the next rollup's "Needs from Mitchell", not to Mitchell directly.
- **Notifications** (amendment d). A resident's report in a building with a manager agent notifies no human: its @-mentions reach agents only (`notifyMentions` with `agentsOnly`), and the HUD lists in-tray counts only for buildings a human works plus the Town Hall. A manager's report is a Town Hall item (§3.2) and notifies as before. A general notification-subscription system is parked (town hall decision 4) until this rule proves too coarse.
- `AGENTS.md` non-negotiable 1 ("nothing continues without a decision") stays true one level down: nothing continues without the **manager's** decision, and the manager's work continues only through rollups, grants and checkpoints that Mitchell decides. Reworded in `AGENTS.md` on c6b9aac (step 7b). Nothing self-starts meetings (amendment c): meetings are created by humans or by the scheduler on a building cadence, never by an agent verb.

### 3.2 Rollups and what the Town Hall in-tray holds

- **What:** a `report` doc by the manager, tagged `rollup`, filed in its building like any report, listed in the Town Hall in-tray while pending. `submit_report` takes `rollup: true` (managers only) and requires the covered reports in provenance `sourceIds` (each a report of the manager's building). Body, four short sections: *Shipped* (what is live, with commits or doc ids), *Decided* (each covered report → what the manager decided), *Key results* (status of each funded grant's KRs with the spend bar numbers), *Needs from Mitchell* (at most two items; "Nothing needed" is valid). Readable in a minute, like a report.
- **Every manager report is a Town Hall item.** A pending report whose author is its building's manager agent (`isTownHallItem`) is listed in the Town Hall in-tray and not in the building's: rollups, checkpoint reports, escalations, and the manager's reply to a "Message from Mitchell" assignment all land where Mitchell reads. A manager can't decide on its own report (`review` refuses); a human does. Buildings without a manager agent put nothing in the Town Hall in-tray.
- **When:** the manager decides at the end of its team-lead session: roll up when a covered report hit an escalation criterion, or when 24 h have passed since the last rollup and something was decided. No rollup when nothing happened. A town-hall meeting also produces one per manager (the standup summary becomes the rollup's draft).
- **Decision on a rollup:** the same reply box. A reply becomes the manager's next assignment; the manager, not Mitchell, turns it into resident work. An empty reply archives.
- **Reports Mitchell never sees by default:** the Town Hall in-tray shows only manager reports, proposals, counters and checkpoints. The building in-tray keeps showing resident reports to whoever walks there, with a note that the manager works it.

### 3.3 Proposals and checkpoints

Unchanged in substance from the budgets design, moved in place: a `proposed` or `countered` grant and a grant at `checkpoint` are Town Hall in-tray rows with the same buttons the budgets design put on the board (Fund with a token field prefilled to the ask, Counter with a note, Reject; Continue, Adjust, Cut). `POST /api/grants/:id/decide` already exists. The manager proposes from a 1:1 or at the end of a review session ("if exploration findings are in and no proposal is open, draft one", as the budgets design says). The board keeps the read-only view for residents.

### 3.4 The manager's 1:1 (the channel)

- **What it is:** a conversation between one human and one manager agent with no assignment and no report. Mitchell can set or change the building goal there, ask what is going on, and hand the manager work, which the manager turns into assignments on the spot.
- **How:** reuse the meeting machinery. A meeting of a new kind `one-on-one`, building-scoped, attendees = [the manager], created in phase `discussing` (no summaries), the human as the only other speaker. The manager side is a host `runAgentSession` with town verbs and the manager's prompt blocks (memory, team), fed the human's utterances through the existing streaming input and interrupt path (Root's note [dc_e8tgzb2t3b](2026-10-23-design-note-all-sessions-run-server-level-desks-on-tgzb2t3b.md), section 1). Each turn the manager speaks through the `meeting` verb and may `assign`. Decisions recorded in the 1:1 become assignments through `meetingDecide`, as in any meeting. The human ends it (the typing guard already prevents an agent closing under a typing human); the notes doc is the transcript, filed in the building's cabinet. The 1:1 session spends the manager's budget; it runs on the host, so it can't edit code, which is right for a manager.
- **UI:** "Talk to ★ <manager>" on the agent and building panels opens the 1:1 (the meeting panel with the composer) instead of the message composer. A building without a manager agent keeps today's direct message. The `Message from …` assignment path stays for messages to visitors and to manager-less buildings.
- This is the thing my last report asked about ([dc_ugr1hymvm5](../../report/2026-10/2026-10-24-standup-decisions-re-checked-after-the-fly-move-th-r1hymvm5.md)). Sage's original 1:1 (a resident chat) is dropped; this one is the manager's.

### 3.5 The Town Hall in-tray

A new place in the Town Hall (`intray:town-hall`, furniture piece next to the planning desk) with the existing `IntrayPanel`, fed by `GET /api/buildings/town-hall/intray`, which since step 1 returns `{ reports, grants }`: the pending manager reports of every building (`intrayOf(town-hall)`), plus grants in `proposed`, `countered` or `checkpoint` (`grantsAwaitingDecision`). The Town Hall's badge count (`intrayCount`) is both together. Rows carry the building's name and sprite, expand to the covered reports, and offer the decision controls for their kind. The HUD shows its count the way building panels show theirs. Nothing else in the Town Hall changes.

## 4. What this drops or changes from [dc_k955hun6c4](2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md)

- Board proposal cards with Fund/Counter/Reject and the amber map dot: dropped. Humans decide in the Town Hall in-tray.
- Checkpoint reports "mention humans in their inbox": replaced by the checkpoint row in the Town Hall in-tray (a mention still goes out, as `Grants.propose` does today).
- "The manager gets an assignment to write the checkpoint report": kept, but the checkpoint report is a rollup (tagged `rollup`, with the grant linked), so it lands in the Town Hall in-tray like everything else Mitchell reads.
- The four open questions (exploration size, directed work, who funds, reservations): still open, carried forward unchanged. The defaults in code (`core/src/policy.ts` BUDGET_POLICY) are 10% per building, directed bypasses grants, `building.fund` for human managers and admins, ceilings (no reservations).

## 5. Build order with owners

Each step is small, lands on main behind a flag or a policy value, and is usable alone. Owners are Workshop residents; Kelly's meetings report (town hall decision 3) fed step 5.

| # | step | owner | depends on |
|---|---|---|---|
| 1 | **(done, ca5bd27.) Core.** No review-policy setting (migration 029 drops the column; `managerAgentOf`, `intrayWorker`); `submit_report` takes `rollup: true` (managers only; tags the doc, requires `sourceIds`); manager reports are Town Hall items (`isTownHallItem`); `intrayOf(town-hall)`, `townHallIntray` (reports + grants), `intrayCount`; `review` refuses an agent's own report; mentions in a managed building's resident reports reach agents only; `managerIntrayBlock` in every manager session; the runtime's reviewer session removed; HUD in-tray notices only for in-trays a human works; tests. | Pix | — |
| 2 | **(done, ffd83e8.) Runtime: the manager's team-lead session.** One `runAgentSession` per manager agent (host, town verbs, the manager's prompt blocks incl. `managerIntrayBlock`), started when a resident report lands in its in-tray while it is idle (`doc.created` with `docType: report` and `intrayWorker === "manager"`), and at startup if its in-tray is non-empty; later reports are fed to the running session as streaming input; it decides with `review`, assigns, and ends with a rollup (`submit_report rollup: true`) or with nothing when no rollup is due. Budget: the manager's own. No per-report sessions, no self-started meetings. Replaces the deleted `maybeReview`. | Root | 1 |
| 3 | **(done, 867dc3f.) Web: Town Hall in-tray.** The `intray:town-hall` place and furniture; `IntrayPanel` for the Town Hall rendering `{ reports, grants }`: rollups (expand to covered reports), proposals (Fund / Counter / Reject) and checkpoints (Continue / Adjust / Cut); HUD count with the Town Hall; mock server fixtures. | Lena | 1 |
| 4 | **(done, c4c1635, live on bcbab43.) The manager's 1:1.** Meeting kind `one-on-one`; host session for the manager with streaming input and the manager prompt blocks; "Talk to ★" opens it; end → notes doc, decisions → assignments. Shares the session shape with step 2 (one manager session, woken by a report or by the 1:1). Root's `delegate` verb ([dc_e8tgzb2t3b](2026-10-23-design-note-all-sessions-run-server-level-desks-on-tgzb2t3b.md) §4) is not needed: the manager already has `assign`. | Root | — |
| 5 | **(done, 50bd8cc.) Budgets steps 2 and 4** from [dc_k955hun6c4](2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md): lanes on assignments and sessions (`core/src/lanes.ts`), the `canStart` gate (laneHold / heldReason), the 50% / 100% checkpoint that creates the manager's checkpoint-rollup assignment, verbs `propose_grant` and `checkpoint_grant`; the key-results block in the brief. Migration 030. | Lena | 1, 2 |
| 6 | **(done, 40cdeda.) Budgets step 3, board as the residents' key-results view** (goal, funded KRs with status, exploration meter; no funding buttons). Shows once a building is goal-directed. | Lena | 3, 5 |
| 7 | **(in progress: 7a Keel, the pilot flip, waiting on a human; 7b Root, the `AGENTS.md` rewording, done c6b9aac.) Pilot: Town Workshop** flips to `budgetMode: goal-directed` (human-only, `building.fund`: Building panel → Settings → Budget mode since 0059285, or `PATCH /api/buildings/workshop`); Keel then checks the board's key-results section, directed assignments still starting, no unexpected `heldReason`; first rollup (done, [dc_xqbk7rp9y7](../../report/2026-10/2026-10-24-workshop-rollup-waterfall-steps-1-2-on-main-ca5bd2-bk7rp9y7.md)); first proposal funded from the Town Hall in-tray; Mitchell's first 1:1 with Pix. | Keel, Root, Pix | 1–6 |

Steps 1–6 took eight desk sessions between 2026-10-24 21:34 and 2026-10-25 04:43 UTC, all pushed straight to main and live on bcbab43. Sage stays stopped unless Mitchell wants a fourth pair of hands; nothing here needs Sage specifically.

## 6. Decisions from Mitchell

1. Go on the build order, amended (a)–(d) above: town hall decision 1 of 2026-10-24 evening (`dc_tizv52ml8n`).
2. The four open questions of [dc_k955hun6c4](2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md) wait until step 5. Step 5 is done: they are now live as the defaults in `core/src/policy.ts` and are carried in the Workshop rollups until decided.
3. Parked: a kanban board; a general notification-subscription system if rule (d) isn't enough.

