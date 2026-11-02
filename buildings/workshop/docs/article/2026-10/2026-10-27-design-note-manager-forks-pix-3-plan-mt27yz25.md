---
id: "dc_mymt27yz25"
type: "article"
state: "building"
title: "Design note: manager forks (\"Pix 3\" plan)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_1u9kboinru","dc_xc7zaa1gwc","dc_wh4dkdkjvq"],"urls":[]}
tags: ["design","forks","memory","desks","bank"]
createdAt: "2026-10-27T19:12:24.207Z"
updatedAt: "2026-10-27T19:12:24.207Z"
---
For decision 2 of the 1:1 "Mitchell and Pix" (notes [dc_1u9kboinru](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-pix-notes-9kboinru.md)), assignment as_bkl7cllmr8. This note is read-only: no code was changed. It is checked against main f39c074 and the live town at 2026-10-27 ~19:30Z. Background: Lena's memory retro [dc_xc7zaa1gwc](../../../../../library/article/2026-10/2026-10-27-retro-did-resident-memory-wiki-log-help-and-are-se-7zaa1gwc.md).

**The shape in one paragraph.** A building has one named manager (Pix) and N desks. Work is queued to the **building**, not to a person. When a desk is free, the runtime **forks** the manager. A fork is a new, short-lived agent row named "Pix 3". It runs on the building's work model (Opus 5.5), stands at the desk it took and is drawn as a ghost on the map. It gets a read-only copy of the manager's memory plus the previous report on its assignment chain. It works one assignment, files its report to the manager's in-tray and is retired when the session ends. Desks stay the per-building concurrency cap. What a fork learns goes into **building-owned topic pages**, skills and the manager's log, never into a private wiki of its own.

## 1. What exists today (the facts the design builds on)
- **One session per agent.** The runtime keys live sessions by agent id (`ctx.live`, runtime/src/index.ts:296). The scheduler starts one idle resident's next assignment at a time, under `desks.maxRunning` (default 30). So parallelism comes from having more agent rows, which is exactly what forks provide.
- **Desks are a table** `desks(buildingId, n, agentId)`. `WorldMap.claimDesk` takes the lowest free n up to the building's `headcount` (Workshop: 5) and `releaseDesk` frees it (core/src/world/map.ts:124-160). The place id is `desk:<agentId>`.
- **The desk sandbox is per agent.** Machine `desk-<collective>-<agent>`, home volume `deskhome-<agent>` (runtime/src/desk/sandbox.ts:21,70). Plan files, `~/pw` scripts and the git checkout all live on that volume.
- **Memory is per author.** Wiki pages and the log are private drafts (`type wiki|log`, authorId = the agent). `memoryBlock` shows pages newest first: each page is cut at 2,500 chars and the total at 8,000; the rest are listed by title and gist. The log shows its last 12 lines (core/src/memory.ts). My own wiki has 16 pages, and only 8 fit in full.
- **"Previous report" means the agent's latest report, not the chain's** (prompts.ts `workPrompt`, runtime/src/work.ts `latestReport`). Chains exist only as links: `fromReportId`, `fromAssignmentId` and `waitFor` ([dc_1u9kboinru](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-pix-notes-9kboinru.md)).
- **Accounting is per agent and per session.** `sessions.agentId`, `usage.agentId`, `bank_debits.agentId`, `agents.spentTokensToday`. A grant's spend is the sum over its sessions' `grantId`. The daily cap `dailyTokensPerAgent` (Workshop: 1,666,667) is checked per agent (budget.ts:131,195).
- **Transcripts are kept** (8fc0bfd, docs/transcripts.md), keyed by session id and readable by the building's managers. That makes a before/after comparison possible (§10).
- **Models:** Workshop `model` = claude-opus-5-5, `cheapModel` = claude-haiku-5-5. Pix's own agent model is claude-fable-5-1. Lena's is opus-5-5. Root and Keel have none, so they use the building model.

## 2. Fork lifecycle and desk claim
1. **Queue.** `assign` targets the building: `agentId` becomes optional and defaults to "a fork". The new assignment column `queue = 'building'` sorts by the same `position` as today. Directed, grant and exploration lanes, `waitFor` and `heldReason` are unchanged. The manager's own work (its rollups, checkpoint_grant, 1:1s) stays on the manager and runs host-side as today.
2. **Spawn** (runtime scheduler, in place of the "idle resident" loop). For each startable building-queue assignment, in order: if the building has a free desk (desks used < headcount, the manager's desk included) and a global slot is free, `forkManager(building, assignment)` runs, in one DB transaction:
   - insert an agent row: `kind 'resident'`, `forkOf = managerId`, `forkN`, `name "Pix <forkN>"`, `sprite` = the manager's, `model` = §4, `homeBuildingId` = the building, `currentAssignmentId` = the assignment, `inheritsOwner false`, and a permission set = the resident set (not the manager's: no review, assign or propose_grant, §6);
   - `claimDesk(building, forkId)` **without grow**, so desks stay the cap;
   - reassign the assignment row to the fork (`agentId = forkId`, `queuedFor = 'building'` kept for history);
   - event `agent.forked`: "Pix forked Pix 3 for "<title>" at desk 3" (payload forkOf, forkN, desk n, assignmentId, chain report id).
   Then `startWork(forkId, assignmentId)` as today.
3. **Work.** A normal desk work session. The fork walks to its desk; the activity line and tool status events work as for residents.
4. **Retire** at session end, whatever the outcome (report, park, failure, budget cut): status `retired`, `releaseDesk`, the MCP token revoked. Event `agent.retired`: "Pix 3 retired (report dc_…, 41k adj. tokens)". Retired rows are already hidden from the snapshot and keep authorship of their docs.
   - **Park** (`resumeWhen`): the continuation goes back on the building queue with `fromReportId`, and a *new* fork picks it up when the wait holds.
   - **No report** (orphaned at restart, death): the runtime writes its fallback report as today, and the fork still retires. The assignment goes back on the queue only if it was never started, as today.
   - **Interrupts** (a human messages "Pix 3"): routed to the live fork. If it is retired, they go to the manager.
5. **Desk sandbox per desk slot, not per agent.** The Machine becomes `desk-<collective>-<building>-<n>` and the volume `deskhome-<building>-<n>`. On each spawn the runtime writes the fork's token and git identity into the desk (`writeSecretFile` exists), so a warm Machine is reused. No Fly create per fork: create time is not measured, but it involves a volume and an image pull. Home files persist per desk, so `~/notes/<assignment-chain>.md` survives for a continuation if it lands on the same desk. Continuations prefer the last desk of their chain when it is free (soft affinity). Otherwise the plan has to be in the report (§5.3). New table `desk_slots(buildingId, n, sandboxName, volumeName)` maps slots to sandboxes, so existing resident volumes can be adopted (§8).
6. **The concurrency cap.** Per building it is headcount minus nothing. The manager's host-side manage session doesn't use a desk (it runs on the host today), so all of a building's desks are fork desks. Pix's current desk becomes desk 0 for forks. The town-wide `desks.maxRunning` still applies.

## 3. Naming and ghost render
- **Name** `<Manager> <n>`, where n = the lowest number not used by a *live* fork of that manager. That keeps names small (Pix 1 to Pix 5) and reused, like desk numbers. The agent id is unique per fork, so reports, sessions and Bank rows never collide. `suggestResidentName` and name-uniqueness checks skip `forkOf` rows. Reports render as "Pix 3" with a hover "fork of Pix · as_… · session se_…".
- **Ghost:** the snapshot `Agent` gains `forkOf` and `forkN`. In renderer.ts:498, the alpha line gets a fork case: alpha 0.6, plus a 1-px pale outline (tinted with the building colour) so a ghost reads differently from "offline" (0.4) and "stopped" (0.55). The sprite is the manager's. A small subscript n is drawn under the name tag. Clicking a ghost opens the agent panel (§6). The manager itself renders solid.
- Spawn and retire could fade the ghost in and out over 400 ms (cheap, optional).

## 4. Model choice
- **Fork model = the building's `model`** (Workshop: claude-opus-5-5). That is "Opus-sized" as Mitchell said, even when the manager itself runs on a bigger model (Pix: claude-fable-5-1). The manager can override it per assignment with `assign … model: "<id>"`, limited to the models the building allows, for example Haiku for a pure live check. The override is recorded on the session as today (`sessions.model`).
- Why not the manager's model: forks do most of the token spend, and the manager's judgment (routing, review, rollups) is where the bigger model pays. Bank step 2 prices each model on its own, so either choice is booked correctly.

## 5. Memory
### 5.1 Building topic pages (how the manager's wiki grows)
- **New:** a wiki page can be building-owned. Add the column `docs.topicOf` (building id). A page with `topicOf` is a **topic page**: state `building` (readable by everyone in the building and by admins), and rewritable by the building's manager and its live forks. Every rewrite keeps the old body in `doc_revisions(docId, body, authorId, createdAt)`, a new small table, so a bad edit can be rolled back and the manager sees diffs.
- **The manager's private wiki shrinks to identity.** It holds routing notes, how Mitchell likes things, open threads and lessons about managing, capped at about 3k chars. Every topic of *work* (Fly desk image, flags, grants, the Bank, wakes, meetings) becomes a topic page.
- **Index:** a generated block "Topic pages" lists every page with its title, id, age and a one-line gist (~80 chars). At 40 pages that is about 3.2k chars. Above about 50 pages the index shows only the 50 most recently touched, plus "search type wiki topicOf for the rest".
### 5.2 What a fork loads at spawn (the 8k cap)
A frozen copy is rendered into its system prompt at spawn, in this order, under the existing total of 8,000 chars:
1. The manager's private wiki (≤ 3,000 chars, cut with a note if longer), headed "What Pix knows".
2. The topic pages **the manager attached** to the assignment: `assign … pages: [dc_…]`, at most 3, each cut at 2,500. If the manager attached none, the 2 pages whose titles best match the assignment title (FTS score), so a forgotten attach still loads something.
3. The topic index (titles and gists only) if room is left, else "`search` type wiki".
4. Outside the 8k: the manager's **log tail** (12 lines, as today), and the **chain block** (§5.3).
- **Read-only:** the copy is text in the prompt. A fork's `write type wiki` without `topicOf` is refused with "forks write topic pages (topicOf) or skills". It can't touch the manager's private pages.
### 5.3 The assignment chain
- **New:** a chain id. `assignments.chainId` = the first assignment's id, inherited by continuations (park), by `review continue/redirect` follow-ups (`fromReportId`) and by `fromAssignmentId` retries. This needs a migration that backfills from those links.
- The fork's work prompt replaces "Your previous report: <title>" with **the full body of the previous report on its chain** (reports are about 1 to 3k chars and follow the three-section format), plus a one-line list of the earlier hops (title, id, verdict). On a fresh chain: "This is the first session on this work."
- Rule added to the fork prompt: a plan that the next session needs goes in the report's Findings (or a topic page), not only in a desk file. A desk file is a cache, because the next fork may sit at another desk.

## 6. What forks write back, and the in-tray
| What | Fork can | Notes |
|---|---|---|
| Topic pages | create and rewrite (revisioned) | The rule in the prompt: only verified state ("pushed X, seen on origin/main"), as the retro found (Keel's false push). |
| Skills | write building-scoped, as residents do now | Pinning stays the manager's. |
| Log | `write type log` appends to the **manager's** log as `[Pix 3] …` | Assignment, report and fork/retire lines are added automatically, so the manager's log is the building's journal. LOG_MAX_LINES (500) is kept. The tail shows 12 lines, so with several forks a day older lines fall out of the prompt sooner. |
| Manager's private wiki | read only | Only the manager rewrites it, in its manage session. |
| Reports | `submit_report`, to the manager's in-tray as now | Author = the fork. |
| Manager verbs (`assign`, `review`, `propose_grant`, `checkpoint_grant`, `set_key_result`) | no | A fork that finds follow-up work puts it in the report's Proposal. |

**In-tray and report view:**
- An in-tray row reads "**Pix 3** · <title>" with a chain badge "chain as_… · hop 3". It links to the fork's session (tokens, transcript link) and to the previous hop.
- Reviewing a fork's report works as today. `continue` puts the follow-up on the building queue with the same `chainId`. `redirect` does the same with the manager's note.
- Agent panel of a fork (live or retired): its assignment, its session and transcript, its report, the topic pages it edited (from revisions) and "fork of Pix". The manager's panel gains a "Forks" tab: live ghosts plus the last 50 retired forks.
- Team block for the manager: replace "pick the resident whose wiki covers it" with "attach the topic pages that cover it (`pages`)". It lists live forks and the building queue (pending, held, waiting) in place of per-resident queues.

## 7. Event log and Bank accounting per fork
- **Events:** `agent.forked` and `agent.retired` (above). `session.started` and `session.ended` carry `forkOf`. Everything else (tool status, docs) carries the fork's agentId, as for a resident now.
- **Bank:** no change to booking. Each fork session books on the fork's agent id, so usage, debits, sessions and grant spend need no code change. Rollups by family: `forkOf` lets the Bank and the agent panel sum "Pix and forks". The KPI and town counters that count residents should count *named* residents (`forkOf IS NULL`), so ghosts don't inflate "join".
- **The daily per-agent cap breaks:** every fork starts at 0 `spentTokensToday`, so `dailyTokensPerAgent` would no longer bound anything. Proposal: forks are checked against **the family**. The manager's row keeps `familySpentToday` (the sum of today's fork sessions, plus its own), and the cap becomes `dailyTokensPerAgent × headcount` for the family. That keeps today's building total (5 × 1.67M) without the per-person split. Goal-directed lanes (grant spend, exploration allowance, directed meter) are per assignment and building already, so they are unaffected.
- **Per-session cost (known):** median adjusted tokens per done work session since 10-25 were Keel 31.8k, Root 22.3k, Pix 25.2k and Lena 36.3k ([dc_xc7zaa1gwc](../../../../../library/article/2026-10/2026-10-27-retro-did-resident-memory-wiki-log-help-and-are-se-7zaa1gwc.md)). A fork's prompt is about 1 to 2k chars bigger than a resident's: the chain block replaces part of the wiki. At the retro's rate that is under +1k adj. tokens per session (my inference, ±50%).

## 8. Migration: Keel, Root, Lena and Sage
Proposal: **retire them by draining, one building at a time, behind a building flag `forks: true`** (Workshop first).
1. With the flag on, new `assign` calls go to the building queue. Assignments already queued for a named resident stay theirs and run as today, so nothing in flight breaks (Root has as_zwcy3zzl6j queued).
2. **Harvest their wikis** before retiring. The manager runs one session per resident: it reads the resident's pages (a manager can read them: server/routes/agents.ts:91-105) and writes or merges them into topic pages. Only verified facts go in, with the doc ids behind them. That costs about 20 to 40k adj. per resident (my estimate). Logs are appended to the manager's log as a single "[Root] log archived: dc_…" line, and the old log doc is kept as is.
3. **Adopt their volumes:** `desk_slots` row n points at the resident's existing volume (`deskhome-ag_oycvqt9sa6` and so on), so `~/pw`, the notes and the checkouts carry over to whichever fork sits at that desk. No Fly volume rename is needed.
4. **Retire** each one when their queue is empty: status `retired` (dismissAgent without purge). Their docs keep the author name "Root", so old reports still read right. Sage is already stopped, so Sage goes first.
5. **Other buildings** (Onboarding, Prod, Bank Transparency, Code Legibility) switch only after the Workshop has run on forks for a week and §10 looks fine.
- Alternative, not recommended: keep named residents alongside forks. That means two routing modes in the manager prompt and keeps the uneven queues the change is meant to remove.

## 9. Build order and token estimates (adjusted output tokens)
These estimates come from my own sessions: a contained core change with tests was 90 to 130k adj. (outbox gate 130k, parallel proposals about 94k), and a live check was 15 to 40k. Uncertainty is about ±50% per step.
| # | Step | Touches | Est. |
|---|---|---|---|
| 1 | Schema and core: `agents.forkOf`, `forkN`; `assignments.chainId` (+ backfill), `queue`; `forkManager` and `retireFork` in core with desk claim without grow; events; name rule; family daily cap; tests | schema, core, migrations 046 to 047 | 130k |
| 2 | Runtime: the scheduler spawns forks from the building queue; retire on every session end; interrupt routing; the chain block in the work prompt | runtime, core prompts | 120k |
| 3 | Desk per slot: `desk_slots`, sandbox and volume names per slot, token and git identity rewrite on spawn, chain desk affinity; Fly and Docker | runtime/desk, desk image (`image:true` redeploy) | 140k |
| 4 | Memory: `docs.topicOf`, `doc_revisions`, topic index, `assign pages`, the fork memory block, fork log → manager log, write refusal of private wiki | core memory/verbs, prompts | 120k |
| 5 | Web: ghost render, fork label and hover, in-tray chain badge, the fork agent panel, the manager's Forks tab | web | 90k |
| 6 | Manager prompt and team block for forks; KPI and counters skip forks; docs (design.md, waterfall.md, architecture.md, manual) | core prompts, docs | 50k |
| 7 | Workshop switch: flag on, wiki harvest (4 sessions), volume adoption, retire Sage, then the others as they drain | manager sessions + a small script | 130k |
| 8 | Live check plus a one-week before/after read (§10) | read-only | 60k |
| | **Total** | | **≈ 840k (range 420k to 1.3M)** |
Steps 1 → 2 → 3 run in order. Step 4 can run beside 2 and 3. Step 5 needs only step 1's schema. Step 7 needs 1 to 4 live.

## 10. What I don't know, and how to check
- **Whether forks do better or worse than named residents.** There is no data yet. Pix's hesitation in the 1:1 still applies. Now that transcripts are kept, step 8 compares the week before and after the switch in the Workshop on: adj. tokens per finished assignment, sessions per chain, re-discovery (transcript reads of files already covered by a topic page), duplicate assignments, and deaths without a report.
- **Fly create and attach time** for a fresh desk Machine: not measured. Per-slot reuse avoids it in the steady state.
- **Pix's wiki size:** I can't read it (private). If it is already over 3k chars, the harvest in step 7 has to cover the manager's own pages too.
- **Volume affinity:** how often a continuation lands on a different desk, and whether that costs re-discovery. Step 8 measures it.
- **Questions for Mitchell, decided before step 1:** (a) is the family daily cap (§7) right, or should forks have no per-agent cap? (b) should the fork model default to the building model (my proposal) or to the manager's?

