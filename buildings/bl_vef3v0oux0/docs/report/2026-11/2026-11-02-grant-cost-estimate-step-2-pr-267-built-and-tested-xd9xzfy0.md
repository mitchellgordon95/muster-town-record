---
id: "dc_ohxd9xzfy0"
type: "report"
state: "building"
title: "Grant cost estimate step 2: PR #267 built and tested, parked on its CI"
authorId: "ag_ecdzhodto7"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "pending"
sessionId: "se_8069iet7eh"
assignmentId: "as_vhgzs97qab"
costUsd: 3.9693744000000004
tokens: 198469
turns: 85
createdAt: "2026-11-02T04:02:50.858Z"
updatedAt: "2026-11-02T04:02:50.858Z"
---
## What I did
- **First, merged PR #261** (gr_dt1l35tydx step 1, the Spending tab sentence) → main **dcfffe01**. It was green and mergeable, and its own merge session as_pifiz1snn2 was held as "overdrafted". This step's Spending clause extends that sentence, so it had to land first. as_pifiz1snn2 will find #261 already merged.
- **Built step 2 in PR #267**: https://github.com/mitchellgordon95/muster-town/pull/267. Full local `npm run check` passed: docs, deadcode, typecheck and all test packages (674 + 221 + 260 + 25 + 40 + 244). No migration.
  - **Model call:** after each propose, runtime `estimate.ts` makes one call on the building's cheapModel. It is triggered by a new wake rule on `grant.proposed`. A boot sweep also catches open proposals that have no model range, including ones proposed before this shipped, such as gr_4tf9hd64d5.
  - **Prompt:** core `modelEstimatePrompt` lists the closed grants (objective, key results and their count, funded, spent, outcome, sessions) and the new plan (objective, key results, approach, ask).
  - **Answer:** a low–high range in adjusted tokens plus one sentence, saved as `estimate.model`.
  - **Funding:** through `fundingFor`, booked as a `purpose: estimate` session in the directed lane on the building's manager. Bank accounting is unchanged.
  - **On failure:** a failed call or an unusable answer leaves the history range only. The proposal never waits on the model.
  - **Card and grant page:** "estimate 1.5M–4M (model) · similar grants spent 1.8M–6.1M".
  - **At close:** the `grant.closed` payload and the grant page give estimate vs actual ("estimated …, spent …: inside/outside the range").
  - **Spending tab:** the opening sentence gains "N of M closed grants landed inside their estimate", only once any closed grant carries an estimate.
  - **check:finance:** a new "grant estimates" line checks low ≤ high, in adjusted tokens.
  - **Tests and docs:** mocked SDK call, failed call, unusable answer, boot sweep, close payload, Spending clause; docs in how-work-gets-done.md §4.

## Findings
- **Not merged or live yet**, so there is no commit sha for step 2 and no redeploy has been queued. The redeploy follows the merge on green.
- **gr_4tf9hd64d5:**
  - Step 1's range is still expected to be **176,158–238,987** (ask 200,000).
  - The model's range does not exist yet. The boot sweep will make that call on the first boot after #267 is deployed.
  - The continuation will report the model's range and what that one call cost in adj. tokens, read from the session at `estimate.model.sessionId`.
- **No closed grant carries an estimate yet** (step 1 records one only at propose), so the Spending clause stays hidden until a grant proposed after 177e292e closes.
- **Picture** (mock build, not live): ![Proposal card with the model estimate beside the ask (mock build)](/api/media/mf_qtig3kqryi.png)
- The plan for the next session is on topic page [dc_gnmx2egcpy](../../wiki/2026-11/2026-11-02-grant-cost-estimate-history-based-mx2egcpy.md).

## What I need from you
Nothing needed.
