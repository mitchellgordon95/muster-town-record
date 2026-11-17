---
id: "dc_ap066avext"
type: "report"
state: "building"
title: "Docs in docs/ drift from the code unchecked; proposed gr_8k0nn380tp to extend check:docs"
authorId: "ag_mba3s6qt8t"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done: findings in dc_yzmmfpnepp, proposal gr_8k0nn380tp filed. I verified the DOCS list (scripts/check-doc-refs.ts:26-33) and that packages/schema/src/rollup.ts and scripts/check.sh are gone from main 7a886f8. Rendered the money ask on gr_8k0nn380tp (Fund / Reject, recommend Fund). Nothing further to queue until Mitchell decides."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-17T03:36:06.799Z"
sessionId: "se_inenw6pqdy"
assignmentId: "as_dgv69032kr"
costUsd: 0.9805783
tokens: 49029
turns: 19
createdAt: "2026-11-17T03:34:42.684Z"
updatedAt: "2026-11-17T03:36:06.799Z"
---
## What I did
I ran a copy of scripts/check-doc-refs.ts over every docs/*.md, not only the docs it checks today. Then I filtered out the false positives and checked camelCase identifiers against the code. Findings are in [dc_yzmmfpnepp](../../note/2026-11/2026-11-17-doc-drift-outside-check-docs-13-docs-in-docs-cite-mmfpnepp.md). I proposed gr_8k0nn380tp under gl_i9gm1fodgo: one M step, 150,000 tokens.

## Findings
- check:docs reads README, CLAUDE, AGENTS, the muster-town SKILL.md, manual.md and docs/invariants/*.md. It does not read the other 28 docs, docs/architecture.md included.
- The raw run over all of docs/ gave 477 problems, mostly false positives. 118 were table names flagged as verbs, and many were package-relative paths like `core/domain.ts`. After resolving those, 37 path references (about 25 distinct paths) are still missing in 13 docs. Examples: `packages/core/src/rollup-asks.ts`, `packages/schema/src/rollup.ts` and `RollupCards.tsx` (deleted by 01253807), `kpis.ts`, `plan.ts`, `finance-pools.ts`, and `scripts/check.sh` (now scripts/check.ts).
- 35 of about 3,700 camelCase identifier spans name nothing in packages/ or scripts/. Examples: `familyCap`, `reviewPolicy`, `messageAgent`, `drawPool`.
- The invariants docs are already well covered: 7 docs, 97 invariants, 287 `- Test:` lines, all checked. So under gl_i9gm1fodgo the remaining gap is the other docs in docs/.
- The grant extends the check with package-relative and suffix path resolution, an identifier rule, and a `Status: history` skip for postmortems and retired designs. It fixes all the findings in the same PR. If the identifier rule needs more than 10 allow-list entries, it ships paths only.

## What I need from you
Fund or reject gr_8k0nn380tp.
