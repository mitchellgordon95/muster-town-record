---
id: "dc_kft2962dq9"
type: "report"
state: "building"
title: "Job abstraction plan: draft filed (dc_ejm1j7m3r8), inventory table unfinished after the circuit breaker"
authorId: "ag_hinlwbx0c0"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_ewxnhs90cq","mt_db6itzy2br","dc_ejm1j7m3r8","dc_pqrcy8pmke"],"urls":[]}
tags: []
verdict: "continue"
decision: "redirect"
decisionNote: "Finish the job abstraction plan (dc_ejm1j7m3r8) and file it for Mitchell. Do it in this one session, inline, with NO subagents (the last session lost ~497k tokens to four parallel inventory subagents whose results never came back; the circuit breaker stopped it). Steps: (1) build section B, the inventory table (file:line → new place or retired), by grep + Read per file over the ~30 files the draft's \"still to inventory\" list names; stop adding rows once every writer of ask words, every in-tray row writer, every rollup reader and every budget rule is mapped, even if some minor files are left as one \"unmapped\" line. (2) Adjust section C's step estimates only where B turns up paths the draft missed. (3) Rewrite dc_ejm1j7m3r8 in place (same id) so it stands alone: A, B, C, D, plus a one-screen summary at the top that Mitchell can read in a minute: what the one object and one loop are, what goes away (rollups, the five ask-word writers), the total cost and the natural stop point after step 5, and the one question he must answer. (4) Rewrite the topic page dc_pqrcy8pmke. (5) File the report with verdict pivot (plan and cost, no code, no PR). Budget guard: if you pass 250k tokens, stop inventorying, write what you have, and file."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-10T20:21:35.554Z"
sessionId: "se_z52ps7tbfa"
assignmentId: "as_qganrass1j"
costUsd: 11.2288177
tokens: 886615
turns: 7
createdAt: "2026-11-10T20:21:03.174Z"
updatedAt: "2026-11-10T20:21:35.554Z"
---
## What I did
I read both 1:1 transcripts (mt_ewxnhs90cq, mt_db6itzy2br) and checked the cited code anchors at main b12cc372. I drafted the plan and published it to the cabinet as [dc_ejm1j7m3r8](../../note/2026-11/2026-11-10-plan-the-job-abstraction-draft-inventory-table-unf-m1j7m3r8.md), with a topic page at [dc_pqrcy8pmke](../../wiki/2026-11/2026-11-10-job-abstraction-plan-as-qganrass1j-rcy8pmke.md). The circuit breaker stopped the session at about 497k tokens. Most of that went to four parallel code-inventory subagents, and their results never came back. No code was changed and there is no PR.

## Findings
- **Drafted in [dc_ejm1j7m3r8](../../note/2026-11/2026-11-10-plan-the-job-abstraction-draft-inventory-table-unf-m1j7m3r8.md):**
  - **A, the abstraction:**
    - A `jobs` table with one status machine and a budget rule per job: chunk, ceiling, per-run, pocket, plus a new `building` rule for the manager's own thread.
    - An `entries` table with structured `moved` fields: stepsDone, krClaimed, `left`, topUp, proposed, shipped.
    - `answer(entry)`, which settles each entry at one of three levels: code, then manager, then the human at the nearest captained node. Passing an entry up spawns nothing.
    - Asks get `kind` (open, resize, act, rule) and `sourceEntryId`. They are never written from a template.
    - `chainConflict(goalId)` checks every path that attaches a building to a goal. Captains sit only on a building's goal or above it.
    - A Secretary per captain, the Secretary as Town Hall manager, and residents able to publish.
    - The mermaid stretch, done as a markdown fence with no new doc type.
  - **C, migration:** 10 PR-sized steps.
    - Steps 1-2 are independent: the chain rule (M, 120k) and Secretary as manager plus resident publish (M, 130k).
    - Steps 3-9 are a chain, L each: jobs and entries read-only, submit_report writes entries, one answer loop, asks over the thread, the building thread replaces rollups, Secretary per captain, delete the compatibility layer.
    - Total about 3.0M adjusted tokens; the stretch item is S, 50k. Natural stop point after step 5.
  - **D, prompt cache:** a table showing where each new field and view lands. The fixed explanation goes in the system prompt; thread, queue and job state go in the first message.
- **Not done: B, the full inventory table.** 13 rows are verified with file:line, for example:
  - wakes.ts:35-54 (town-written in-tray rows)
  - asks.ts:290 (the "Fund it" template recommendation)
  - asks.ts:445 (the "Your call" parser)
  - docs.ts:360-370 (the rollup fold)
  - secretary.ts:509/560/274 (rollup prose readers)
  - the boot repairs in invariants/asks.md #12-14

  Also found: there is no "what is left" field today. The draft's B section lists the roughly 30 files still to map.
- Next session: build B inline without subagents, adjust the C estimates if more paths turn up, rewrite [dc_ejm1j7m3r8](../../note/2026-11/2026-11-10-plan-the-job-abstraction-draft-inventory-table-unf-m1j7m3r8.md), then file the report with verdict pivot so it reaches Mitchell before any code.

## What I need from you
Nothing needed.
