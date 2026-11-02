---
id: "dc_kfss21u5w3"
type: "report"
state: "building"
title: "Code Legibility rollup: doc-drift check ready in PR #58, needs a human to add the CI step"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_vwld1s9k6j"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/58"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Code Legibility: gr_z9xj51uox3 (architecture docs with diagram, 400k adjusted tokens) is funded by Mitchell. Mitchell re-issues the desk GitHub token with Workf"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:43:04.356Z"
sessionId: "se_848p05zl9z"
createdAt: "2026-10-27T06:58:28.552Z"
updatedAt: "2026-10-27T17:43:04.356Z"
---
## Shipped
- `npm run check:docs` (scripts/check-doc-refs.ts, commit 3abbf00) is ready in draft PR #58. It checks file paths, npm scripts, verbs and `mcp__town__` tool names in README, CLAUDE.md, AGENTS.md and SKILL.md, and paths and scripts in docs/manual.md. It passes on today's docs. When we broke 9 references on purpose, it reported all 9 and exited 1. It is not merged and not in CI yet.
- The split with Onboarding is agreed with Kelly and written up in [dc_mu57k5t71o](../../note/2026-10/2026-10-27-doc-drift-vs-onboarding-copy-drift-who-owns-what-c-57k5t71o.md): we own mechanical references, Onboarding owns whether the copy is right.

## Decided
- [dc_vwld1s9k6j](2026-10-27-doc-drift-split-agreed-with-kelly-check-ready-in-d-ld1s9k6j.md) (Mara, doc-drift check): approved. The work is done; the only remaining step needs a human (below).

## Key results
- No funded grants yet. gr_z9xj51uox3 (architecture docs, for kr_dctpbbwtno) is still awaiting your decision.
- kr_oubxzkl4n6 (doc-drift CI check): the check exists. It meets the key result once it runs in CI and main is green.
- Spend today: exploration 0 / 828,571 tokens; directed 111,857 tokens.

## Needs from Mitchell
1. Add the 2-line `npm run check:docs` step to .github/workflows/ci.yml (the text is in PR #58), then merge PR #58. Desk tokens lack the GitHub `workflow` scope, so no agent can push changes to workflow files.
2. Fund, counter or reject gr_z9xj51uox3.
