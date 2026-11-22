---
id: "dc_6b62k7etda"
type: "report"
state: "building"
title: "PR #552: deploy waits run live checks; pass closes the step with no session, fail wakes it with results"
authorId: "ag_rv110dx5k1"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-22T18:42:28.880Z"
sessionId: "se_cu3e726bjx"
assignmentId: "as_7atth3v7vi"
costUsd: 1.9715903
tokens: 98580
turns: 30
createdAt: "2026-11-22T18:42:28.838Z"
updatedAt: "2026-11-22T18:42:28.880Z"
---
## What I did
Built step 1 of gr_qg42b4guky in PR https://github.com/mitchellgordon95/muster-town/pull/552. It covers the schema, core waits.ts, ask-checks.ts, the runtime tick, tests, invariant 12 and docs/wakes.md. `npm run check --fast` is green on the desk (7m24s), and the 4 new tests pass.

## Findings
- **Shape.** `{deploy: sha, checks: [{kind: url|api, ref, status?, contains?}], verifies: [kr]}`. Both lists take at most 5 entries.
- **Same runners as the asks.** The checks reuse the ask-check runners through a new `runLiveCheck` in core ask-checks.ts. url gains an expected status and a `contains` text, which reads the body through net-guard safeGet. api runs in-process through `world.host.apiGet`, which is `app.inject`. That call works outside a request, so the stop condition did not apply and there is no second fetcher.
- **Pass.** Core `checkWaits` runs the checks only once the deploy is live, one run per assignment at a time. The runtime `track`s each run. When all pass, the parked work closes as done with no session. The job thread gets an entry "live checks passed (N); verified kr_…" that lists each check with its value. Each `verifies` key result turns met (event `kr.verified`), and a grant step queues its next step. closeMerged now shares this close path.
- **Fail.** The wait clears. The continuation's description lists each check, what it expected and what the live town returned. A "live checks failed" entry goes on the thread, and no key result moves.
- **Other grants refused.** `validateWait` refuses a `verifies` key result of another grant, or `verifies` without checks. submit_report and assign pass the grant to it.
- **Deploy never live.** No check runs, and the wait expires after 24 h like any other.
- **Design choice:** a passing live check also verifies an *open* key result, because naming it in `verifies` counts as the claim. Ask claims still leave open key results alone.
- The plan for step 2 is in topic page [dc_88e2pvpm7a](../../wiki/2026-11/2026-11-22-live-checks-on-a-deploy-wait-e2pvpm7a.md).

## What I need from you
Nothing needed.
