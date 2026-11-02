---
id: "dc_vwld1s9k6j"
type: "report"
state: "building"
title: "Doc-drift split agreed with Kelly; check ready in draft PR #58, CI step needs a human"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_mu57k5t71o","dc_i2c7in8y77"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/58"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done. The CI step needs workflow scope, which only a human has, so it goes to Mitchell in the rollup."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-27T06:58:20.939Z"
sessionId: "se_hsrtscofn0"
assignmentId: "as_1rjan88pov"
costUsd: 1.4423055
tokens: 85253
turns: 42
createdAt: "2026-10-27T06:55:03.879Z"
updatedAt: "2026-10-27T06:58:20.939Z"
---
## What I did
- Recorded Kelly's agreement in [dc_mu57k5t71o](../../note/2026-10/2026-10-27-doc-drift-vs-onboarding-copy-drift-who-owns-what-c-57k5t71o.md), including her two caveats, and replied to her.
- Built the mechanical doc-reference check for kr_oubxzkl4n6: `npm run check:docs` (scripts/check-doc-refs.ts), commit 3abbf00, draft PR https://github.com/mitchellgordon95/muster-town/pull/58.

## Findings
- **What it checks:** README, CLAUDE.md, AGENTS.md and skills/muster-town/SKILL.md for paths, `npm run` scripts, verbs, `mcp__town__` tools and CLI commands. docs/manual.md for paths and scripts only, per Kelly: it names UI buttons.
- **Verified:** it passes on today's docs. I broke 9 references on purpose (a path, a script, a verb, an MCP tool, a SKILL.md tool line, a manual link and a manual script). It reported all 9 and exited 1. A made-up verb in manual.md was correctly ignored.
- **Gaps:** a bare `data/` like the one from sweep 1 isn't caught, and single-word verbs in prose aren't checked.
- **Not in CI yet:** GitHub rejected the push because the desk token lacks the `workflow` scope, so no desk can edit .github/workflows. The PR describes the 2-line step to add before `npm run typecheck`. Without that step, the PR's README line saying CI runs check:docs isn't true yet.
- **Main was red, now fixed upstream:** main CI failed on ee536a5 (run 40461507512; the web mock still returned `proposal`). 6c80fe4 fixed it on main while I worked, so I dropped my duplicate fix.
- **Repo moved:** it now lives at github.com/mitchellgordon95/muster-town.

## What I need from you
Add the `npm run check:docs` step to .github/workflows/ci.yml (text in PR #58), then merge PR #58.
