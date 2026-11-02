---
id: "dc_zapg9h6g9x"
type: "report"
state: "building"
title: "Rollup Needs now refuses anything already in the in-tray or outbox; the town appends \"Already waiting in your in-tray\" (8a91952 on main, live check parked)"
authorId: "ag_qotmfczwg2"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. 8a91952 on main: the Needs rule in code (refuse gr_/open requests/pending rollups by id, warn on >2 items, append the \"Already waiting\" line), tests green on the desk, manual at 1,891/1,900 words. The live check is already parked as as_eoorqpvd73 on {deploy: 8a91952}, so no new assignment. Rollup 30 (as_rzgy2cp5xf, 10-29 20:00Z) will be the first rollup under this rule and must show the generated line; if CI on 8a91952 is red by then, the rollup prep queues the redeploy after the fix."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T22:29:25.746Z"
sessionId: "se_jdrhmf8gcz"
assignmentId: "as_m96b70d021"
costUsd: 1.4391893
tokens: 71959
turns: 34
createdAt: "2026-10-28T22:29:13.007Z"
updatedAt: "2026-10-28T22:29:25.746Z"
---
## What I did
I extended the rollup-format code from 689761f (as_kyqoc5s9s7) and pushed **8a91952** straight to main. It has a Needs rule in schema and core, the generated in-tray line, the manager prompt text, docs (manual, waterfall, log) and tests. The `redeploy` tool refused: a fork lacks `town.redeploy`. CI redeploys main on green, so I parked on deploy 8a91952.

## Findings
**The rule** (`ROLLUP_NEEDS_RULE`, `packages/schema/src/rollup.ts`). The manager in-tray block quotes it word for word, and every refusal repeats it:
> "## Needs from Mitchell" carries at most 2 items, and only what has no other channel: a decision Mitchell reserved, a question needing an answer in words, a 1:1 invite, or a real-world action with no outbox request. Never an open grant proposal or checkpoint (gr_…), an open outbox request or a report already in the Town Hall in-tray (dc_…): Mitchell sees those there, and the town appends an "Already waiting in your in-tray" line listing them.

**What `submit_report` with rollup:true now does** (`packages/core/src/verbs/docs.ts`):
- **Refuses** a rollup whose Needs section names any of these, and lists the offending ids with the reason (for example `gr_x (a grant proposal in the Town Hall in-tray)`). The manager fixes it and resubmits in the same session.
  - A grant awaiting a human: proposed, checkpoint, or closed-as-done with a claimed key result.
  - An open outbox request.
  - A pending Town Hall report.
- **Exemptions:** countered grants (they wait on the manager), and a checkpoint or close rollup naming its own grant.
- **Detection is by id only.** A Needs item that says "fund the Bank grant" without its gr_ id is not caught. The prompt carries the rule for those.
- **Warns** (still files) when Needs has more than 2 list items.
- **Appends** a generated line at the end of Needs, computed at submit time for the manager's building: `_Already waiting in your in-tray: N proposals (gr_…), M requests (dc_…), K rollups (dc_…)._`, or `_Nothing else waiting in your in-tray._` when all three are zero.
  - Proposals are that building's grants with status `proposed`. Requests are open requests filed in that building. Rollups are its pending rollups.
  - The manager doesn't write the line. A report can't be rewritten through `write` either: that tool refuses type report.
- **Prompt:** the Needs bullet in `managerIntrayBlock` now carries the rule. The refusal sentence names the new case. `ESCALATION_CRITERIA` now says that an outbox request or grant proposal reaches Mitchell on its own and stays out of Needs.
- **Docs:** `docs/manual.md` Rollups now says "only what has no other channel, then a line listing what already waits in your in-tray". The manual is at 1,891 words against the 1,900 cap. `docs/waterfall.md` §3.1–3.2 and `docs/log.md` are updated too.

**Tests (on the desk):**
- `core/test/rollup-format.test.ts`: 7/7, 2 of them new. They cover:
  - a pending gr_, an open request and a pending rollup are each refused;
  - a reserved decision, a 1:1 invite and a decided resident report pass;
  - the generated line reads exactly `1 proposal (gr_…), 1 request (dc_…), 1 rollup (dc_…)`, and the zero case reads "Nothing else…";
  - 3 Needs items trigger the warning;
  - the line is inserted correctly when Needs isn't the last section.
- Also passing: core lanes 22/22, verbs 23/23, prompts 8/8, kr-authors 2/2, runtime manage 6/6, web manual 3/3. `tsc --noEmit` passed for schema and core.

**Should be live:** 8a91952, once CI's redeploy runs. Not verified live yet.

**Live check still to do (next session):**
1. GET /api/health `commit`, then `git merge-base --is-ancestor 8a91952 <commit>`.
2. Read the next Workshop rollup (due ~10-29 20:00Z, as_rzgy2cp5xf) and confirm its Needs ends with the generated line.

The rule is also on topic page [dc_oghes5lgud](../../wiki/2026-10/2026-10-28-grants-key-results-and-the-town-hall-in-tray-hes5lgud.md).

## What I need from you
Nothing needed. If CI on 8a91952 is red, Pix should queue a redeploy after the fix, since I can't.
