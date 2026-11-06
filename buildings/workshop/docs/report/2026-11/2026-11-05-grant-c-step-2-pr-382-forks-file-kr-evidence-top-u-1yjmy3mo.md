---
id: "dc_en1yjmy3mo"
type: "report"
state: "building"
title: "Grant C step 2: PR #382 (forks file KR evidence + top-up with submit_report; card/deck list the grant's reports), parked on CI"
authorId: "ag_bjw4epgqkr"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Step 2 of gr_95svkzi4l6 built as PR #382 (8bc0899), parked on its CI; the continuation as_wpy81v6su4 waits on {pr: 382} and merges if green. Nothing else to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T23:30:42.132Z"
sessionId: "se_wylqhe2ou2"
assignmentId: "as_2z4odi0fw2"
costUsd: 3.1859029
tokens: 159295
turns: 64
createdAt: "2026-11-05T23:30:34.339Z"
updatedAt: "2026-11-05T23:30:42.132Z"
---
## What I did
Confirmed PR #381 merged (4ab6187 on origin/main). Built step 2 of gr_95svkzi4l6 on top of it as one commit 8bc0899, pushed, opened draft PR https://github.com/mitchellgordon95/muster-town/pull/382. Local `npm run check`: docs, deadcode, typecheck green; tests 809/810, the one failure was the old "A top-up: not stated" deck assertion, which I updated (that file plus the new tests re-run green, 16/16). Parked on the PR's CI.

## Findings
- **submit_report** (schema `ReportKrEvidence`, `ReportTopUp`): optional `keyResults: [{id, status: not-started|on-track|at-risk|claimed, evidence ≤2000}]` and `topUp: {tokens, buys}`. `Grants.checkReportEvidence` runs before the report is filed: the session's lane (else its assignment's) must be grant, the grant funded or held, every KR an open KR of that grant. Otherwise the call is refused with the reason and nothing is filed. `fileReportEvidence` runs inside the submit transaction: status, note "<evidence> (report dc_…)", statusBy = the fork, a `kr.updated` event with the reportId. topUp replaces the grant's line. A grant-lane report with neither field is filed with a warning; the body is unchanged.
- **Top-up lifetime changed:** a continue or adjust now clears the line, and a hold keeps it. Before, the hold cleared it, which would have wiped what the forks filed.
- **evidence()** adds `reports` (the grant's sessions' reports: title, author, verdict, at), `filed` (an agent set a KR) and per-KR `by`. **Deck slide + in-tray card (Places.tsx)** show "No evidence filed by the forks" when nothing was filed, then the KR lines "… (who)", then the grant's reports, then the top-up line only when one was filed.
- **Fork prompt:** a static `GRANT_EVIDENCE` paragraph in workSystemPrompt (cache-safe) with the field shapes.
- **Tests:** core/test/grant-evidence.test.ts (6: accepts; refuses another grant's session, exploration, another grant's KR, met; warning; evidence with and without filing, latest top-up wins; hold keeps / continue clears; prompt), the server submit_report route accept + refuse, and the web card with and without evidence.
- **Docs:** how-work-gets-done §4/§6 (how evidence reaches the card), invariants/grants.md 8 + new 8a, architecture, goal-directed-budgets, log line. `checkpoint_grant` is left only in history (log, waterfall, migration 085, the "verb is gone" test).
- Once live, I couldn't file this session's own KR evidence: the live server doesn't have the fields yet. This step serves kr_13txlz2pnc, kr_z0gd978wbg and kr_jnkstduw76.
- Topic page [dc_nqgbjho18g](../../wiki/2026-11/2026-11-05-grant-c-self-assembling-checkpoint-card-reserve-gbjho18g.md) rewritten.

## What I need from you
Nothing needed.
