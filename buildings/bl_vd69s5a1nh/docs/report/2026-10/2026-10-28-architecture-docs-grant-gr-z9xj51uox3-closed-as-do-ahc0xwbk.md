---
id: "dc_nqahc0xwbk"
type: "report"
state: "building"
title: "Architecture-docs grant gr_z9xj51uox3 closed as done (309k tokens returned); sweep proposal gr_8ve21typt6 in the in-tray; Finn on the CI-flake root cause"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_a90unrt5ju"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"1:1: Mitchell and Mara\": Mara: add key result \"Unused code paths get found and removed\" (dead-code sweep report, knip/ts-prune check green in CI on main, >=3 removals merged) to the bui"
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-28T17:53:37.272Z"
sessionId: "se_bq7xzfpie7"
createdAt: "2026-10-28T17:42:10.644Z"
updatedAt: "2026-10-28T17:53:37.272Z"
---
## Shipped
- Nothing new on main this session. docs/architecture.md (PR #59, f39c074) is the evidence behind the close below; all four invariants docs are on main at e7fabc2 (closed last rollup, kr_bo4codoha8 marked met by Mitchell 17:32Z).
- Finn's abstraction sweep 1 is filed: [Abstraction sweep 1: candidates](../../note/2026-10/2026-10-28-abstraction-sweep-1-candidates-4mlk2wuh.md), 10 ranked candidates with file:line, risk and ±50% token estimates. Two real drifts found: schema's DeskControl lacks the `interrupts[].now` the server sends, and the desk's SDK copy has diverged from the runtime's.

## Decided
- [dc_a90unrt5ju](2026-10-28-abstraction-sweep-1-10-candidates-filed-dc-0q4mlk2-0unrt5ju.md) (Finn, sweep 1) → approve. Turned into proposal gr_8ve21typt6.
- Closed gr_z9xj51uox3 (architecture map) as done: 90,852 of 400,000 tokens spent, 309,148 returned to the Bank. kr_dctpbbwtno is now claimed; this report is its close report.
- Proposed gr_8ve21typt6 for kr_doa59kdway, 260,000 tokens: consolidate candidates #1 (desk contract → schema, fixes the `now` drift), #2 (whereOf in core/table.ts, 7 sites), #3 (permissions.requireAdmin, 9 server sites; the 3 in core/bank.ts left alone), plus #7 (DAY_MS) if tokens remain. Held back because they touch Bank/token-accounting code: #4 desk SDK copy and #6 Bank view types.
- Assigned Finn exploration as_sevasd12il for kr_cm5qb2wqh7: root-cause the v12.test.ts "table desk_slots already exists" failure (main run 40612811023) and tabulate the last 20 main runs. Findings only; no fix to Workshop code without asking.
- Town hall mt_m5vub4jd41 decision 5: nothing for me beyond the proposal above.

## Key results
- kr_dctpbbwtno (architecture docs): claimed. Grant gr_z9xj51uox3 closed, 90,852 / 400,000 tokens.
- kr_bo4codoha8 (invariants): met. gr_jd1q10o5rh closed (323,284 spent of the adjusted 2,000,000).
- kr_oubxzkl4n6 (doc-drift CI): done via PR #58, never granted; not yet marked met.
- kr_doa59kdway (abstraction sweeps): sweep report in; proposal gr_8ve21typt6 open (260,000 ask).
- kr_cm5qb2wqh7 (CI green without reruns): exploration started today.
- Spend today by lane: exploration 90,479 / 828,571 tokens (Finn's sweep); directed 0.

## Needs from Mitchell
1. Mark kr_dctpbbwtno met or missed from the in-tray: open docs/architecture.md on main and check the diagram renders and it reads in about 10 minutes.
2. Decide gr_8ve21typt6 (fund, counter or reject). If you also want the Bank-touching candidates (#4, #6) done, say so and they go in a second proposal.
