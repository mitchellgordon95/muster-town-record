---
id: "dc_6elfdumhqg"
type: "report"
state: "building"
title: "Checkpoint card shows evidence: PR #266 open, waiting on CI"
authorId: "ag_vu0luzlh0b"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_7b4zc7yja3","dc_oghes5lgud"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/266"]}
tags: ["parked"]
verdict: "continue"
decision: "pending"
sessionId: "se_4o29ur85d7"
assignmentId: "as_vdhsw3q0zq"
costUsd: 3.744659499999999
tokens: 187233
turns: 72
createdAt: "2026-11-02T03:58:25.613Z"
updatedAt: "2026-11-02T03:58:25.613Z"
---
## What I did
Built the checkpoint card change Mitchell asked for in 1:1 mt_7b4zc7yja3 across core, server and web, with tests and docs. Merged main into the branch: main had taken migrations 083 and 084, so mine is 085, and I resolved a GrantRow conflict so main's "likely cost" span stays. `npm run check` passes locally (1,462 tests). Opened draft PR https://github.com/mitchellgordon95/muster-town/pull/266. Parked on its CI.

## Findings
- **core**: `checkpoint_grant` now requires `whatTopUpBuys` and `topUpTokens` once per held checkpoint. You give both or neither. A new hold clears them. They aren't asked for once a human has already continued or topped the grant up.
  - Migration 085 adds `grants.topUpTokens` and `grants.whatTopUpBuys`.
  - `GrantView.evidence` (`Grants.evidence`) holds, per key result, a verdict plus the manager's note: claimed or met = shipped, on-track or at-risk = partly, not-started or missed = not shipped. It also holds spent vs granted, the top-up line and the Shipped titles from the checkpoint report.
  - A proposal gets `evidence` too, when the same building's latest grant on the same goal stopped at its checkpoint (cut or spent). That stands in for "a proposal that re-asks money for the same work". Nothing links the two explicitly, so it's a heuristic.
- **deck slide** (core review-deck.ts): starts with lines like `1. ✓ shipped: <note>`, then Spent, then "A top-up of N tokens buys: …" ("A top-up: not stated" on old checkpoints), then the Shipped titles, then Your call. The plan comes last.
- **in-tray row** (web Places.tsx GrantRow): shows the evidence block, then Continue / Adjust / Cut. The key results and stop condition sit under a fold.
- The checkpoint assignment text and the manager prompt now tell managers to write a note per key result and the top-up line. Updated docs/how-work-gets-done.md (§4 and the §6 checkpoint bullet), docs/invariants/grants.md and docs/log.md.
- **Tests**: core `lanes.test.ts` (required line, cleared at the next hold, evidence) and `review-deck.test.ts` (new slide; re-ask proposal); server `grants.test.ts` (in-tray and `/api/review-deck` both return evidence); web `checkpointEvidence.test.tsx` (lines, not stated, fold order, proposal).
- In the first full check, `backup.test.ts` failed once on timing (131 ms gap, limit 100 ms). It passed when re-run alone, and the full check after the merge was green.
- **Next session** (resumes on PR #266 CI):
  1. If green, mark ready, merge, `redeploy`, and note which commit should be live.
  2. Add a Shipped line for rollup 38 to [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md).
  3. Rewrite topic page [dc_oghes5lgud](../../wiki/2026-10/2026-10-28-grants-key-results-and-the-town-hall-in-tray-hes5lgud.md): add the checkpoint rule (forks give a note per key result, plus `whatTopUpBuys`/`topUpTokens` once) and the evidence card.
  4. If CI is red, fix it on the branch and park again.

## What I need from you
Nothing needed.
