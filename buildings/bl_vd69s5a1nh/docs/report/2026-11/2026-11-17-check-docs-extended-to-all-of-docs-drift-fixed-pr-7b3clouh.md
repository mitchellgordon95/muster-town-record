---
id: "dc_6o7b3clouh"
type: "report"
state: "building"
title: "check:docs extended to all of docs/; drift fixed; PR #490 parked on CI"
authorId: "ag_jwy5h6o5or"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T03:55:10.128Z"
sessionId: "se_mowyt0gm4e"
assignmentId: "as_namvln7hok"
costUsd: 2.6110609000000005
tokens: 130553
turns: 51
createdAt: "2026-11-17T03:55:10.090Z"
updatedAt: "2026-11-17T03:55:10.128Z"
---
## What I did
I extended check:docs to every doc in docs/ and fixed all the drift it found, in draft PR #490 (https://github.com/mitchellgordon95/muster-town/pull/490, commit ddbe793c). The full `npm run check` passed on my desk. I parked this session on the PR's CI.

## Findings
- **Rules.** The rules moved to scripts/doc-refs.ts so the tests can run them on a fixture repo. scripts/check-doc-refs.ts is now only the CLI (manual cap, log rule). The check now reads 36 docs: README, CLAUDE, AGENTS, SKILL and every docs/**/*.md except log.md and log.d/. The verb rule stays only where it was before.
- **Paths.** A path resolves as written, then package-relative (`core/x.ts` → packages/core/src/x.ts), then as the suffix of any tracked file. It also handles `:12` line suffixes, `<x>` placeholders inside segments, `dc_…` link targets and mermaid fences. Allow rules: collective and export layout files, build output, the skill-bundle example paths in skills.md, and `fly.toml` in self-host.md.
- **Names.** A camelCase `code span` must be declared, keyed, read or quoted in packages/*/src or test or scripts/, or be a migration column. Comments don't count: stripping them caught `familyCap` and `intrayRow`, which only comments still mention. No allow-list entries were needed, so the stop condition (more than 10) was not hit. Two external API names (`recordVideo`, `getMonitors`) are now written as plain text. The rule I wrote down in the script: a name that is gone or not built yet goes without backticks.
- **History skip.** `Status: history` in a doc's first lines skips it. I marked docs/waterfall.md and docs/legible-delegation.md, which held 22 of the findings (all about rollups).
- **Drift fixed.** 13 docs, 88 findings before the fix. A few examples:
  - kpis.ts is gone from architecture.md.
  - `scripts/check.sh` is now `scripts/verify.sh` in skills.md.
  - `intrayRow` is now `messageEntry` in architecture.md.
  - messageAgent, wakeKey, dailyLimitTokens, plan.ts, finance-pools.ts, DashboardPanel.tsx and others are now unbackticked as removed or not built.
  - Grep checks from the key results: kpis.ts appears 0 times in architecture.md, and scripts/check.sh 0 times in skills.md.
- **Tests.** packages/core/test/check-scripts.test.ts has a new block "check:docs: every doc in docs/" with 6 tests: the scope, a deleted path fails, path resolution and examples pass, an unknown camelCase name fails, `Status: history` skips, and the repo's own docs pass.
- **Check timings on my desk:** docs 1s, deadcode 9s, typecheck 38s, tests 7m17s.
- **Key results:** both are ready to claim once the PR merges. kr_42oj33018m: check:docs passes with the new scope. kr_r7gd2fzw10: the fixture tests run in the PR's CI.

## What I need from you
Nothing needed.
