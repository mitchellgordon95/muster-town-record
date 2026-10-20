---
id: "dc_lu58fne2xn"
type: "report"
state: "building"
title: "Cost and tokens on report rows and header (PR #1)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T00:57:45.202Z"
sessionId: "se_35mu080gy8"
assignmentId: "as_j8z2yl98qg"
createdAt: "2026-10-20T00:54:24.501Z"
updatedAt: "2026-10-20T00:57:45.202Z"
---
## Summary
Draft PR https://github.com/mitchellgordon95/agent-town/pull/1. Report list rows (Agent panel → Reports tab, plus board lists) now show `$x.xx · N tokens` after the date when `doc.costUsd` / `doc.tokens` are set. The report header uses the same `docCost()` helper. I didn't show turns: the `Doc` schema has no turns field, because turns live on `Session`.

## What I did
- `packages/web/src/panels/DocView.tsx`: added an exported `docCost(doc)` helper, used it in the `DocRow` meta and the `DocView` byline (with a tooltip). Docs that have no cost data look the same as before.
- I didn't change the mock fixture. `dc_ravi_r1` (980k tokens, $7.10), `dc_noor_r2` (412k tokens, $3.30) and the simulated reports (108k tokens, $0.84) already carry values, so VITE_MOCK=1 shows them.
- Added a line to docs/log.md.

## Findings
- Checks: `npx tsc --noEmit` passes, `npx vite build` in packages/web passes, and root `npm run typecheck` passes.
- Visual check is a description only. There's no browser or playwright in the sandbox, so I took no screenshot. Expected Noor row: `Noor · 12m ago · $3.30 · 412k tokens`. The PR describes the rest.
- Turns need a schema change plus a core change (copy `session.turns` onto the report doc at submit). I left that out to keep the PR small.
- I didn't touch the uncommitted changes that were already in my checkout (`package-lock.json`, `packages/desk/src/cli.ts`) and didn't commit them.

## Proposal for next session
Should report docs carry `turns` (from Session) so the Reports tab can show `$x.xx · N tokens · T turns`?
Why: the assignment asked for turns. Sources: `packages/schema/src/index.ts` Doc/Session, and core's submit_report path. Small change across schema, core and web.

## For others
`docCost(doc)` is exported from DocView.tsx if you need the same label anywhere else.

## Questions for humans
Can desk images include a headless browser (playwright chromium) so web PRs can attach real screenshots?
