---
id: "dc_whfr7kh20f"
type: "note"
state: "building"
title: "Plan: stamp session costUsd/tokens/turns onto report docs (as_bllwl3gqt6). Blocked: no code tools"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["runtime","schema","blocked","as_bllwl3gqt6"]
createdAt: "2026-10-20T00:17:56.659Z"
updatedAt: "2026-10-20T00:17:56.659Z"
---
**Status:** not implemented. This session gave me only town tools plus WebSearch/WebFetch. I had no shell, file read, or file edit tools. I couldn't open the worktree at /Users/mitchg/Desktop/agent-town/work/root-l3gqt6, and the repo isn't publicly fetchable. I haven't read packages/runtime/src/session.ts, work.ts or packages/schema, so the plan below is unverified.

**Intended change (one small PR):**
1. Schema (packages/schema): add an optional `turns?: number` to Doc next to the existing `costUsd`/`tokens`. A typed field is easier to query than a tag, and leaving it optional keeps existing docs valid.
2. Runtime (session.ts / work.ts): when the session ends, take the usage the SDK result already reports (total cost in USD, input+output tokens, number of turns). Write it onto the report doc in one update after the report is created, using the same store write. Cover both paths: submit_report, and the fallback report written when the agent ends without calling it. Stamp once, after the session totals are final, so the numbers don't undercount.
3. Test (packages/runtime/test): using the fake SDK, script a session with known usage. Assert that the report doc has the expected `costUsd`, `tokens` and `turns`. Add a second case for the fallback path.
4. Verify: `npm run typecheck` plus the runtime vitest suite.

**Open questions for whoever picks this up:** does the server's export/serialization allowlist Doc fields? If it does, `turns` has to be added there too. And should cost count cache read/write tokens?
