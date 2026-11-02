---
id: "dc_rcb6nclr6u"
type: "report"
state: "building"
title: "Code Legibility rollup: 5 key results written, architecture grant proposed, doc-drift split agreed with Onboarding"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_n7ca5a10ld"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Code Legibility: gr_z9xj51uox3 (architecture docs with diagram, 400k adjusted tokens) is funded by Mitchell. Mitchell re-issues the desk GitHub token with Workf"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:43:04.352Z"
sessionId: "se_61j8zvw6ka"
createdAt: "2026-10-27T06:09:24.236Z"
updatedAt: "2026-10-27T17:43:04.352Z"
---
## Shipped
- Nothing went live from this building. [dc_mu57k5t71o](../../note/2026-10/2026-10-27-doc-drift-vs-onboarding-copy-drift-who-owns-what-c-57k5t71o.md) is the ownership split between our doc-drift CI check and Onboarding's copy sweep. It was sent to Kelly.

## Decided
- [dc_n7ca5a10ld](2026-10-27-doc-drift-vs-onboarding-copy-split-by-kind-of-chec-ca5a10ld.md) (Mara, doc drift vs onboarding copy) → **approved**. Onboarding owns whether the developer docs still say the right thing. We own a mechanical CI check for broken path, script and verb references, and it never edits prose. The split stands unless Kelly objects.

## Key results
- I wrote 5 key results from the 1:1 notes [dc_i2c7in8y77](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-mara-notes-c7in8y77.md): kr_dctpbbwtno (architecture docs), kr_bo4codoha8 (invariants docs), kr_doa59kdway (abstraction sweeps), kr_oubxzkl4n6 (doc-drift CI check), kr_cm5qb2wqh7 (CI green without reruns). None has a funded grant yet.
- gr_z9xj51uox3 (architecture docs, 400k tokens) is proposed and waiting for your decision.
- Spend today: exploration 0 / 828,571 tokens; directed 26,604 tokens.

## Needs from Mitchell
- Fund, counter or reject gr_z9xj51uox3. The invariants and doc-drift grants are queued behind it because a building can only have one open proposal.

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_dctpbbwtno: "Humans can understand the system from architecture docs and diagrams: docs/architecture.md shows how the core subsystems (runtime/wakes, assignments & lanes, grants, bank) fit together, with at least one diagram, linked from README and AGENTS.md." (how to check: docs/architecture.md exists on main with a rendered diagram (e.g. Mermaid) naming each core subsystem and how data flows between them; README and AGENTS.md link to it.; from [dc_3pfuorg12c](2026-10-27-draft-key-results-for-code-legibility-and-maintena-fuorg12c.md))
- created kr_bo4codoha8: "Each core subsystem (runtime/wakes, assignments & lanes, grants, bank) has an invariants doc in docs/ saying what must always hold and how it interacts with the others, each invariant named by at least one test." (how to check: AGENTS.md links one invariants doc per subsystem and the links resolve; every invariant cites a test name that grep finds in the test suite.; from [dc_3pfuorg12c](2026-10-27-draft-key-results-for-code-legibility-and-maintena-fuorg12c.md))
- created kr_doa59kdway: "Abstraction sweeps: recurring sweeps find code patterns repeated outside the core subsystems that would be cleaner as a shared abstraction, and the worthwhile ones get moved into a core subsystem." (how to check: A sweep report in the filing cabinet lists candidates with file paths; at least 3 candidates are consolidated into a core subsystem in merged commits on main, with tests passing.; from [dc_3pfuorg12c](2026-10-27-draft-key-results-for-code-legibility-and-maintena-fuorg12c.md))
- created kr_oubxzkl4n6: "Developer docs don't drift from code: a CI check fails when AGENTS.md, CLAUDE.md or README reference a file, script or tool name that doesn't exist (onboarding copy drift is Kelly's, not this)." (how to check: The doc-drift check runs in GitHub Actions on main and is green; deliberately breaking a path reference in a PR makes it fail.; from [dc_3pfuorg12c](2026-10-27-draft-key-results-for-code-legibility-and-maintena-fuorg12c.md))
- created kr_cm5qb2wqh7: "CI on main stays green without reruns: flaky tests get fixed at the root, not retried." (how to check: GitHub Actions for main: the last 20 runs pass on the first attempt (no re-run attempts), e.g. no repeat of the flake in run 40454959781.; from [dc_3pfuorg12c](2026-10-27-draft-key-results-for-code-legibility-and-maintena-fuorg12c.md))
