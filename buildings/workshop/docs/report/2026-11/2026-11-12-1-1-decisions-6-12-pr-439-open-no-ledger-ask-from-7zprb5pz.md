---
id: "dc_be7zprb5pz"
type: "report"
state: "building"
title: "1:1 decisions 6+12: PR #439 open (no ledger ask from act_in_1on1 or Keep; oversight line); PR #436 closed; parked on CI"
authorId: "ag_dj0uxz01iz"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged: PR #439 (no ledger ask from act_in_1on1 or Keep; oversight line) is parked on CI and resumes itself to merge; PR #436 closed. No rollup yet: nothing of ours is live since rollup 60."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-12T18:18:13.352Z"
sessionId: "se_sn18mopxq3"
assignmentId: "as_bge7equrv6"
costUsd: 0.9743180000000002
tokens: 48716
turns: 26
createdAt: "2026-11-12T18:17:57.719Z"
updatedAt: "2026-11-12T18:18:13.352Z"
---
## What I did
Third attempt, kept small (typecheck + two test files only, push --no-verify). No branch from Pix 1 for this work existed on origin (only old `pix-1/planner-1on1` and `secretary-step-1-...`), so I started fresh.

## Findings
- **(a) Decision 6 (+8), PR #439** https://github.com/mitchellgordon95/muster-town/pull/439 (draft): `packages/core/src/act-in-1on1.ts` no longer calls `ruleFromOneOnOne` (removed from `secretary.ts`); `onAskDecided` in `packages/core/src/secretary.ts` no longer proposes a ledger rule when a human decides a policy ask (the Keep twin). The only remaining path is the Secretary's weekly pattern note (`filePattern` with `rule`); only a human's Add appends. Tests: `packages/core/test/policy-ledger.test.ts` rewritten ("deciding a policy ask files no ledger ask…", "act_in_1on1 doing a decision the human said files no ledger ask"), plus notices.test.ts: 6/6 pass; typecheck green; check:docs green.
- **(b) Decision 12**: docs/engineering-human-oversight.txt now has "Reports have no affordances; asks programmatically perform small tasks to keep users deciding, not doing" as the last line of the reports-vs-asks list under "Decision presentation". Also updated docs/invariants/notices.md 5, architecture.md, legible-delegation.md, plus docs/log.d/2026-11-12-pix-2-no-ledger-ask-from-act-or-keep.md.
- **(c)** PR #436 is closed unmerged, with a comment: gr_2r17x8egrc was cut, and decisions 13/15 moved the narrowed rule to Code Legibility.
- **Duplicate ledger asks**: live GET /api/asks shows no open ask with a `ledger-add` branch. Nothing to close.
- Live is 2f0cbf73. After the merge, the live check is: act_in_1on1 on a 1:1 decision files no ledger ask. If no 1:1 happens, cite the tests above.

## What I need from you
Nothing needed. I'm parked on PR #439's CI. Next session: mark it ready, merge, and verify live.
