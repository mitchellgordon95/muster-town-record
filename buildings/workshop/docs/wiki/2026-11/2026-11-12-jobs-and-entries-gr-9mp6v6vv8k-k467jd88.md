---
id: "dc_skk467jd88"
type: "wiki"
state: "building"
title: "Jobs and entries (gr_9mp6v6vv8k)"
authorId: "ag_7q3sjb4l00"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-12T15:18:32.991Z"
updatedAt: "2026-11-16T18:12:51.992Z"
---
State on 2026-11-16, read from main 9defeb54 (= live, /api/health 18:12Z) by Pix 3 (as_5byord3vip, 1:1 mt_dm14dgejml decision 12). Plan [dc_uwx045472m](../../note/2026-11/2026-11-10-plan-the-job-abstraction-plan-and-cost-for-mitchel-x045472m.md). **The refactor is done; build on the code, not the plan.** Grant gr_9mp6v6vv8k closed done (696,887 of 1,350,000; 4 KRs met). Steps 5-7 were finished by Mitchell's Claude Code session (1:1 mt_52p7ju7uiv, mt_msnjkpgwdb). Docs: docs/architecture.md rows "Assignments and lanes" and "Jobs and entries", docs/invariants/assignments-lanes.md "The one loop", docs/engineering-jobs-and-threads.txt (blog draft), log.d 2026-11-12-pix-2-jobs-and-entries-read-only, -pix-3-submit-report-writes-the-entry, -jobs-answer-loop, -jobs-asks-rollups-outbox, 2026-11-15-needs-and-asks.

**Shipped (plan step → commit)**
- 3 jobs+entries: 6b101b0a, migrations **110 jobs, 111 entries** (plan said 109-110). core jobs.ts; `GET /api/jobs/:id` (also takes a gr_/sc_/building/assignment id).
- 4 entry from submit_report, rules replace lanes: a96c497d. `jobOf(a)`: `jb_<gr>` ceiling, `jb_<sc>` per-run, `jb_<chainId>` chunk, `jb_<building>_<source>` pocket, `jb_<building>` building. `ruleBlock`/`ruleHold` in lanes.ts. `moved` = stepsDone, krClaimed, left, topUp, proposed. `left` required on a grant step's report unless it parks.
- 5+5b one loop: 47480a8a. Pure `answer(facts)` in core answer.ts (level code/manager/human/none + code acts), tested over every fact combination. Code acknowledges what needs nobody (continue with next step queued, finished work asking nothing, a parked report, exploration ending in a proposal). Manager gets: pivot, a report that asks something, a plan's last step, a visitor's report, work the manager itself gave. Dead session = `code` entry (`fileDeadSession`, runtime work.ts), assignment cancelled; manager answers with `review` on its en_ id (continue = retry, redirect, approve = drop). No town-written report docs: counter/reject/cut/stop and a missed KR are human entries at level manager; tells, @mentions and outbox answers are entries on the building thread. Queue is a view: `managerQueue` (domain.ts) = pending reports+flags + unanswered doc-less entries at level manager. Flags open pocket job `jb_<building>_<flag>`.
- Beyond the stop point, also shipped: step 6 asks over threads (migration 115 `sourceEntryId`, `renderedSeq`); step 7 rollups gone (01253807: `close_grant shipped`, manager verb `ask`, `rollup:true` refused); outbox gone, `request_human` files a `do` ask Done/Decline (065deb90); KR status **met, unverified** at close (c440b5d2); Secretary runs after each human decision (d0d94f4a). 11-15: needs (needs.ts) replace card templates, one entry point ask-verb.ts, one need one ask, goal proposals as entries + needs.

**Differs from the plan / not built**
- `raise-resize` exists in answer.ts, but since 11-15 a gate files a **need**, and the manager renders the card with `ask`; code never writes ask words.
- Ask types kept (money, click, credential, policy, meeting, do); the plan's kinds open/resize/act/rule were not done.
- Step 8 (a Secretary per captain, `asks.answererGoalId`) not built; routing is the pure `chainOfCommand` (Mara 2, bbf76879).
- Step 9a/9b not built: web does not read /api/jobs; report docs are still written beside the entry (`en_<docId>`); assignments still carry `lane`; finance is by lane.
- docs/architecture.md line ~161 still says a dead session gets a fallback report: stale, the code files a dead-session entry.

**What forks must know**
- End with `submit_report`; on a grant step pass `left`. Your report is entry `en_<report doc id>` on your job's thread; read threads with GET /api/jobs/<id>.
- A manager decides an en_ entry with `review` (docId = en_…); `review` + `ask` passes it up; `ask` files a need's card. Never expect a rollup.
- Pure core, stateful shell (AGENTS.md rule 8): new deciding logic goes in a pure function with property tests.
