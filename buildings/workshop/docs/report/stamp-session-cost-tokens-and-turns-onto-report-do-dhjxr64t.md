---
id: "dc_9wdhjxr64t"
type: "report"
state: "building"
title: "Stamp session cost, tokens, and turns onto report documents — PR #2"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T00:57:55.701Z"
sessionId: "se_lgwvdwzgh3"
assignmentId: "as_m8rls9239b"
createdAt: "2026-10-20T00:55:11.594Z"
updatedAt: "2026-10-20T00:57:55.701Z"
---
## Summary
Done. When a work session ends, `finishWorkSession` (packages/runtime/src/work.ts) now copies the session's usage (tokens, costUsd, turns) onto the report doc it produced. This works for submit_report reports and for both fallback paths (normal and stopped). Draft PR: https://github.com/mitchellgordon95/agent-town/pull/2

## What I did
- schema: added optional `Doc.turns` (int).
- core: added migration `004_doc_turns.sql`. The docs table needs a real column because Table checks its columns against the schema.
- runtime: after `endSession`, the report doc is patched with `{tokens, costUsd, turns}`. This only happens when `doc.sessionId === sessionId`, so an older report is never overwritten.
- tests: new assertions in `packages/runtime/test/work.test.ts` for the happy path (1200 tokens / $0.42 / 4 turns), the fallback (300 / $0.01 / 4) and the stopped fallback (50 / $0.001 / 4), all using the fake SDK.
- Added a line to docs/log.md.

## Findings
- Verification: `npm run typecheck` passes and runtime vitest passes 22/22. I removed the runtime change and re-ran: the 3 stamping tests fail, so they really test the change.
- A core test already fails on main: `packages/core/test/desks.test.ts > work brief > workspace buildings get repoUrl/base/branch/dir`. It expects `git@github.com:...` but gets `https://...` since commit 6f39d85 (desks clone over https). My PR doesn't touch it.
- My checkout had uncommitted changes I didn't make (package-lock.json, packages/desk/src/cli.ts mode change). I left them out of the commit.

## Proposal for next session
Should the desks.test.ts repoUrl expectation be updated to https, matching 6f39d85? It's a one-line fix that makes `npm test` green on main. Main has a red test right now, which hides real regressions.

## For others
Report docs now carry `turns`, along with tokens and costUsd. The web DocView already shows costUsd and could show turns and tokens too (Pix?).

## Questions for humans
None.
