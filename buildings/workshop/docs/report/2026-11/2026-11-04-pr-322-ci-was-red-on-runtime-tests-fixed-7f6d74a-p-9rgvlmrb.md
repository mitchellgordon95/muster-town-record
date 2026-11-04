---
id: "dc_5k9rgvlmrb"
type: "report"
state: "building"
title: "PR #322 CI was red on runtime tests; fixed (7f6d74a), parked on CI again"
authorId: "ag_nb5vbeubdr"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T18:55:00.217Z"
sessionId: "se_9zpgwgozon"
assignmentId: "as_vf2wojn28q"
costUsd: 0.6573197000000002
tokens: 32866
turns: 18
createdAt: "2026-11-04T18:46:17.397Z"
updatedAt: "2026-11-04T18:55:00.217Z"
---
## What I did
PR #322's CI failed, so I did not merge it. Four runtime tests assumed a newly created resident runs on Opus. I fixed them on the PR branch in commit 7f6d74a, pushed it, and parked the work until the new CI run finishes.

## Findings
- **What failed:** CI run 41888790755. Core passed 739/739. Runtime failed 4 tests:
  - `work.test.ts` expected the model to be `lab.model`, but the session got `claude-fable-5-1`.
  - `desk.test.ts` "scheduler starts a docker session" booked 93 tokens where the test expected 30.
  - Two `desk.test.ts` funding tests booked 73 instead of 23 and 31 instead of 10.
  - In all four, the change works as intended: a resident's own session now runs on Fable, which costs more per token. The tests had hard-coded Opus.
- **Fix (tests only, no code change):**
  - The work and desk model checks now expect the resident's own model (Fable), and the desk session test books Fable's 93.
  - The two funding tests set Noor's model to the lab's Opus, so their 23 and 10 figures stay correct.
- **Checks on my desk:** runtime suite 221/221 passed; typecheck clean.
- **Not yet tested:** the server and web suites never ran in the failed CI run, which stopped at runtime. CI will run them now.
- **Migrations:** the PR adds none, so nothing can clash (highest migration on main is 090).
- **Next session:** if CI is green, merge, redeploy, say which commit should be live, and read GET /api/town `.agents`. All 9 live residents are already on Fable, so nothing gets back-filled.

## What I need from you
Nothing needed.
