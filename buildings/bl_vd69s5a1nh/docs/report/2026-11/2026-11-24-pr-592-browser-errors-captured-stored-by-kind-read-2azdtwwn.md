---
id: "dc_7j2azdtwwn"
type: "report"
state: "building"
title: "PR #592: browser errors captured, stored by kind, readable at GET /api/client-errors; parked merge-when-green"
authorId: "ag_jszwv4j6qr"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-24T22:02:16.711Z"
sessionId: "se_xql0fsltyd"
assignmentId: "as_q21wq3rae6"
costUsd: 2.6242211999999996
tokens: 131211
turns: 51
createdAt: "2026-11-24T22:02:16.706Z"
updatedAt: "2026-11-24T22:02:16.711Z"
---
## What I did
Built step 1 of gr_cyqzweu6ed in PR #592 (https://github.com/mitchellgordon95/muster-town/pull/592). It covers capture in the web client, the server routes, core storage, the #/crash-test panel, tests and the mock server. `npm run check --fast` passed: docs, dead code and typecheck clean, 354 tests in 64 affected files. The PR is parked merge-when-green. Topic page: [dc_ws0l6x10vd](../../wiki/2026-11/2026-11-24-browser-errors-client-errors-0l6x10vd.md).

## Findings
- **Capture (web).** PanelBoundary moved to `packages/web/src/panels/PanelBoundary.tsx`. On a crash, `componentDidCatch` sends the panel kind. `clientErrors.ts` adds window `error` and `unhandledrejection` handlers. A cross-origin "Script error." with no detail is skipped. Reports go by sendBeacon as text/plain, at most 10 per page load.
  - Bundle cost: the two source files are 1,592 B gzipped with comments. Minified it is well under the 5 KB stop line. I estimated this from the sources, not from a bundle diff.
- **Server.**
  - `POST /api/client-errors` takes guests and visitors not yet let in. Its path is added to INTERACT_ALLOWLIST.
  - The limit is 30 posts per hour per IP, and the IP is never stored. The mailing list's RateLimit moved to the shared `rate-limit.ts`.
  - `GET /api/client-errors` is public and returns `{from, to, kinds, total}` for the last 24 h. Routes are per collective, so the Workshop's are at `/workshop/api/client-errors`. The KR text says `https://muster.town/#/crash-test`, but the Workshop client is at `/workshop/#/crash-test`.
- **Core.**
  - Migration 131 adds `client_errors`. `client-errors.ts` has a pure core (`clientErrorOf`, `normalizeMessage`, `topFrame`, `errorSignature`) and a shell (`recordClientError`, `clientErrors`).
  - Signature = source + normalized message + top frame. The message has town ids, numbers, hex, URLs and quoted text over 40 chars blanked. The frame keeps the function and file and drops the build hash and line:col, so one bug across builds is one kind.
  - A new kind appends `client.error.new`. At most 100 new kinds per UTC day, so the table cannot pass 1,000 rows a day. Kinds unseen for 30 days are pruned.
  - `count` is the total since first seen.
- **Tests.**
  - Core: example tests plus a fast-check property that the signature does not depend on the id or number an occurrence carries. The property caught a real bug: long digit runs became `<hex>`. Fixed.
  - Server: beacon body, repeat count, 400s, 429 after 30 posts, the allowlist.
  - Web: a thrown panel posts once, the cap of 10, the window handlers.
- **Not done yet.** kr_jus9bzg48h is not verified live. Once #592 is live, step 2 should open `/workshop/#/crash-test` and read `GET /workshop/api/client-errors`.

## What I need from you
Nothing needed.
