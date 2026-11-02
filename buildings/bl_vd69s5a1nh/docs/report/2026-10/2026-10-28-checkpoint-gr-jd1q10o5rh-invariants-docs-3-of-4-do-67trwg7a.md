---
id: "dc_yo67trwg7a"
type: "report"
state: "building"
title: "Checkpoint gr_jd1q10o5rh (invariants docs): 3 of 4 docs live, fix and 5 gap tests on main, bank.md in PR #64; continue with ~60k to finish"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_z2yufo9csy","dc_9wqvb9makh","dc_i8inqcoe5s","dc_ql8ksax71z","dc_0b73jwkty8","dc_wsdch1trh7","dc_dz9a4f8ina"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/62","https://github.com/mitchellgordon95/muster-town/pull/63","https://github.com/mitchellgordon95/muster-town/pull/64"]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Mara: with the extra tokens approved, merge the Bank doc, confirm the doc check passes in CI on main, then close grant gr_jd1q10o5rh with the evidence; tell Nel"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-28T16:16:20.648Z"
sessionId: "se_4510s36upb"
assignmentId: "as_u2r0uvj4d6"
costUsd: 1.3527938499999999
tokens: 27056
turns: 16
createdAt: "2026-10-28T01:17:42.392Z"
updatedAt: "2026-10-28T16:16:20.648Z"
---
## Shipped
- **PR #62 → 499c75d** (live): `docs/invariants/grants.md` (8 invariants, 18 test citations), the one-live-grant-per-key-result fix in `decide` "fund" with test `refuses funding a second live grant on a key result`, tests for adjust-above-spend and a status × action transition table, and the cited-test check in `npm run check:docs` (CI `check` job). Reports [dc_i8inqcoe5s](2026-10-27-invariants-step-1-of-4-grants-draft-pr-62-commit-8-inqcoe5s.md) (Finn), [dc_ql8ksax71z](2026-10-28-pr-62-invariants-step-1-grants-merged-as-499c75d-p-8ksax71z.md) (merge).
- **PR #63 → 7436558** (live; `GET /api/health` commit = 7436558): `docs/invariants/assignments-lanes.md` (8 invariants, 18 citations) and `docs/invariants/runtime-wakes.md` (8, 20), plus tests for the grant lane refusing closed/rejected/draft grants (lanes.test.ts) and the scheduler never starting past `canStart` (runtime queue.test.ts). Reports [dc_0b73jwkty8](2026-10-28-invariants-step-2-of-4-assignments-lanes-runtime-w-73jwkty8.md) (Finn), [dc_dz9a4f8ina](2026-10-28-pr-63-invariants-step-2-assignments-lanes-runtime-9a4f8ina.md) (merge).
- **Draft PR #64 (df90bbb), not merged**: `docs/invariants/bank.md` (10 invariants, 30 citations) and `packages/core/test/bank-invariants.test.ts` (conservation, downtime catch-up credits once, balances floored at 0 after an overshoot). No Bank code changed. Report [dc_wsdch1trh7](2026-10-28-invariants-step-3-of-4-the-bank-and-budget-draft-p-dch1trh7.md) (Finn).
- AGENTS.md on main links the three merged docs; check:docs passes on main locally and in CI. Main CI for our merges passed on attempt 1 (runs 40606365895, 40610344424).

## Decided
- [dc_z2yufo9csy](2026-10-27-invariants-grant-cut-into-4-steps-step-1-grants-fi-yufo9csy.md) (my plan: 4 steps) → approve.
- [dc_9wqvb9makh](2026-10-27-session-ended-without-a-report-invariants-step-1-o-qvb9makh.md) (Finn's step-1 session ended without a report) → redirect: resume from the branch and finish step 1.
- [dc_i8inqcoe5s](2026-10-27-invariants-step-1-of-4-grants-draft-pr-62-commit-8-inqcoe5s.md) (Finn step 1, PR #62) → approve; I took the merge ([dc_ql8ksax71z](2026-10-28-pr-62-invariants-step-1-grants-merged-as-499c75d-p-8ksax71z.md) → approve).
- [dc_0b73jwkty8](2026-10-28-invariants-step-2-of-4-assignments-lanes-runtime-w-73jwkty8.md) (Finn step 2, PR #63) → approve; I took the merge ([dc_dz9a4f8ina](2026-10-28-pr-63-invariants-step-2-assignments-lanes-runtime-9a4f8ina.md) → approve).
- [dc_wsdch1trh7](2026-10-28-invariants-step-3-of-4-the-bank-and-budget-draft-p-dch1trh7.md) (Finn step 3, PR #64) → approve; I assigned myself the merge and close-out as as_k8fa1q38zk (lane grant), which is **held** by this checkpoint.

## Key results
**kr_bo4codoha8** — status **on-track** (set by this checkpoint). Spend: **269,909 / 250,000 tokens at the crossing** (about 296k now, including Finn's step 3 and this session).
How to check: AGENTS.md on main links one invariants doc per subsystem and `npm run check:docs` greps every cited test name. Today it links three (grants, assignments-lanes, runtime-wakes) and says "the Bank is still to come".
Testing plan results:
- Docs exist and are linked: **3 of 4** on main; bank.md in PR #64.
- Every invariant cites a real test: **yes** for the 3 merged docs (56 citations verified by check:docs in CI; Finn broke one on purpose and CI failed).
- One live grant per key result enforced: **yes**, merged in #62 with its test.
- Missing tests added: **8 new tests** cover every gap in [dc_clkaforduh](2026-10-27-invariants-docs-scoped-38-candidate-invariants-9-w-kaforduh.md) (5 on main, 3 in PR #64); main CI green on attempt 1 for both merges.
Remaining to claim: merge #64 (resolve AGENTS.md and docs/log.md conflicts with #63, link bank.md to assignments-lanes.md), confirm check:docs green in CI, close the grant. Estimated 60k tokens.
Other grant: gr_z9xj51uox3 (architecture map, kr_dctpbbwtno) ~91k / 400k, PR #59 merged as f39c074; I may close it early and return tokens once rendering is eyeballed.
Lane spend today: exploration 0 / 828,571 tokens; directed 0 tokens.
Side note for kr_cm5qb2wqh7: main run 40612811023 on the Workshop's commit 0e287b4 failed in runtime `v12.test.ts` ("table desk_slots already exists"); not our code, but it is the kind of first-attempt failure that KR tracks.

## Needs from Mitchell
1. **Continue gr_jd1q10o5rh with about 60k more tokens** (adjust to ~360k total) so as_k8fa1q38zk runs: it merges PR #64, verifies AGENTS.md links all four docs with check:docs green, and closes the grant. Cutting instead leaves bank.md unmerged and the KR unclaimable.
2. A redeploy after that merge, since I don't hold town.redeploy; the live server is on 7436558 and already has the three merged docs.
