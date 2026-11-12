---
id: "dc_id4j1navsg"
type: "report"
state: "building"
title: "submit_report writes the entry; ruleBlock replaces the lanes: PR #435 open, parked on CI"
authorId: "ag_h2fhecot10"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_uwx045472m","dc_k90p1i7q74","dc_skk467jd88"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/435"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #435 parked on CI; the continuation merges and live-checks it. Note the `left` field is now required on step reports: the step-3 fork must know this. Step 3 (gate shows moved.left + the answering loop) queues itself from the continuation's report."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-12T16:31:11.258Z"
sessionId: "se_vwpfiv30km"
assignmentId: "as_arq5feff6l"
costUsd: 2.9643857999999996
tokens: 148219
turns: 49
createdAt: "2026-11-12T16:30:49.561Z"
updatedAt: "2026-11-12T16:31:11.258Z"
---
## What I did
I built step 2 of gr_9mp6v6vv8k (plan [dc_uwx045472m](../../note/2026-11/2026-11-10-plan-the-job-abstraction-plan-and-cost-for-mitchel-x045472m.md) step 4) as PR #435: https://github.com/mitchellgordon95/muster-town/pull/435. The full `npm run check` passed on my desk: docs, knip, typecheck and 2,010 tests. The PR is not merged yet. I am parked on its CI; the continuation will merge it and check it live. I rewrote topic page [dc_skk467jd88](../../wiki/2026-11/2026-11-12-jobs-and-entries-gr-9mp6v6vv8k-k467jd88.md).

## Findings
- **The entry is written live.** `submit_report` now appends `en_<report id>` to its job's thread in the same transaction as the report doc, which is still written. The entry's `moved` holds stepsDone, krClaimed, left, topUp and proposed (an explorer's grant). The answer returns `jobId`. The boot back-fill keeps a live entry's `moved` and only refreshes its level and tokens.
- **`left` is a new field on submit_report.** It is required on a grant step's report. A step report without it is refused with a message that says what to add. A parked report or a rollup does not need it. Seven older test files that file step reports were updated to pass it.
- **Budget rules replace the lanes.** `ruleBlock` and `ruleHold` replace `laneBlock` and `laneHold`, renamed in the code and the docs. Their checks are keyed by `jobOf(a).rule`: ceiling, per-run, chunk, and pocket or building. `jobOf` is the TS twin of the back-fill's SQL, and a test holds the two together. Tests confirm that a grant at checkpoint is still held and that exploration past its cap is still held.
- **Jobs are created as work starts.**
  - `createAssignment` opens the assignment's job. A new explorer gets a chunk job, and a new human source gets a pocket job. The `assignment.created` event carries the `jobId`.
  - Grant events sync the grant's job, so `propose` makes a `proposed` ceiling job and `fund` opens it.
  - A chunk job closes when its last report lands or when the explore tick closes its reservation.
- **Prompt.** The lane line now reads "This session: job jb_… (rule …, pocket …), grant/exploration/directed …". The system prompt adds one fixed sentence on entries and `left`. A new prompts.test case shows the job line is in the first message and not in the system prompt.
- **Not in this step:** the gate card does not show `moved.left` yet. That is the "gate shows it" half of kr_xzdcf7d5i3, and it belongs with the step 3 loop.

## What I need from you
Nothing needed.
