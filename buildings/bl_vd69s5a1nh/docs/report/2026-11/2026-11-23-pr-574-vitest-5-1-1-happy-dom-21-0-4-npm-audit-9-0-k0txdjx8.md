---
id: "dc_ydk0txdjx8"
type: "report"
state: "building"
title: "PR #574: vitest 5.1.1, happy-dom 21.0.4, npm audit 9 → 0; parked merge-when-green"
authorId: "ag_rsekeit520"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:36:18.583Z"
sessionId: "se_nir6e9k403"
assignmentId: "as_7zt33vsg8z"
costUsd: 0.6322727
tokens: 31614
turns: 18
createdAt: "2026-11-23T16:36:18.545Z"
updatedAt: "2026-11-23T16:36:18.583Z"
---
## What I did
I set vitest to ^5.1.1 in core, server, runtime, desk, cli and web, and happy-dom to ^21.0.4 in web. Then I ran npm install and `npm audit fix` with no --force. Typecheck passes, and sampled tests pass on the desk. I opened PR #574 (https://github.com/mitchellgordon95/muster-town/pull/574) and parked it to merge when green. The pre-push fast check passed.

## Findings
- **npm audit:** it reported 9 advisories before (2 critical, 1 high, 6 moderate) and 0 after. The lock now has vitest 5.1.1, happy-dom 21.0.4 and hono 4.13.21.
- **Test files changed: 0.** No package uses poolOptions, and the vitest configs only set `isolate`, which still works in vitest 5. No test needed changes for the new mock behaviour.
- **Desk runs, all with --maxWorkers 1, all passing:**
  - desk: 5 files
  - cli: 2 files
  - runtime: 8 mock-heavy files
  - web: 22 files that use `vi.`
  - core: 9 files
  - server: 4 files
  - Total: 50 files and 447 tests. CI runs the other ~319 files.
- **Fast-check flags:** `--changed origin/main --maxWorkers 1` still works on vitest 5. The pre-push hook (`check --push`) passed when I pushed.
- **CI test-step time against the 105 s baseline: not known yet.** CI had not finished when I parked. kr_ky260b3xlu is measured on the first 5 green main push runs after the merge.
- Rewrote the topic page Dependency advisories ([dc_o70qzef90k](../../wiki/2026-10/2026-10-31-dependency-advisories-0qzef90k.md)). Log entry: docs/log.d/2026-11-23-mara-1-upgrade-vitest-to-5-and-happy-dom-to-21.md.

## What I need from you
Nothing needed.
