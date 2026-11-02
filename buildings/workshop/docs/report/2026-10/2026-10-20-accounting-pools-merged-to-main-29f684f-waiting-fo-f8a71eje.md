---
id: "dc_8sf8a71eje"
type: "report"
state: "building"
title: "Accounting pools merged to main (29f684f); waiting for redeploy to go live"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T23:56:25.900Z"
sessionId: "se_nce2egk38z"
assignmentId: "as_wkc7awpo5j"
costUsd: 0.4842492
tokens: 15701
turns: 17
createdAt: "2026-10-20T23:15:48.797Z"
updatedAt: "2026-10-20T23:56:25.900Z"
---
## What I did
I checked out `feature/accounting-pools`: Root's core commit 990d191 and Lena's web commit 69ed4d3. I ran typecheck, the tests and the build on it. Then I merged it into main as one merge commit, **29f684f**, pushed, and called `redeploy` twice.

## Findings
- Main hadn't moved since the branch was cut, so the merge was clean. The change touches 26 files (+746/−183) and adds migration `023_bank_pools.sql`, which doesn't clash with any existing migration number.
- Typecheck and the web build pass.
- Tests: the core and web suites all pass. One runtime test fails: `packages/runtime/test/work.test.ts`. It fails at my desk because my desk's environment variables leak into it, and it fails the same way on the old main. With a clean environment (`env -i`) all 10 tests in that file pass, so the merge didn't break it.
- The pools are not live yet. The first `redeploy` returned "started", but `/api/health` still showed 2a57a52 after about 5 minutes. The second returned "queued", which I take to mean the restart waits until running sessions are idle. I've paused this work until 29f684f is live. When it resumes I'll confirm it and close this out.

## What I need from you
Nothing needed.
