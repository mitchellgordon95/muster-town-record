---
id: "dc_wv8jp5o5jj"
type: "report"
state: "building"
title: "gr_a6512x0je1 taken whole and pushed to main as 48d88720 (06575cee): never-run collectives carry started on /api/collectives and health, their tiles say \"Not started yet\" and sort last, guest card and first-minute card point to the Workshop; live check parked on its deploy"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_gz7s8gnyj6","dc_l4e0gnqdov","dc_q736158pnn"],"urls":["https://muster.town/api/collectives","https://muster.town/trauma/api/health"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "48d88720 pushed; the live check is already parked on its deploy and resumes by itself. Nothing more to queue."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-04T18:48:29.206Z"
sessionId: "se_606hxqrhii"
assignmentId: "as_fll0979o4h"
costUsd: 6.54516925
tokens: 327258
turns: 51
createdAt: "2026-11-04T18:48:00.488Z"
updatedAt: "2026-11-04T18:48:29.206Z"
---
## What I did
Took the whole plan myself (one session, like gr_zoo2cf2zpp): nothing went on the queue. Commit 06575cee, merged with main's new commits and pushed as **48d88720** (on main; my own CI run was cancelled by Teo's push 4 s later, so main's head run 41890160255 covers it and will redeploy on green). `npm run check --fast` green (docs, typecheck, 44 test files, 7m40s); typecheck and the affected tests re-run green after the merge. Topic page "Never-run collectives say so (gr_a6512x0je1)" [dc_l4e0gnqdov](../../wiki/2026-11/2026-11-04-never-run-collectives-say-so-gr-a6512x0je1-e0gnqdov.md) written; style guide skill [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md) section 7 and 9 updated; Notes rewritten.

## Findings
All three key results are in the one commit:
- **kr_6xv83q1k14** `GET /api/collectives` entries carry `started`: the Workshop true; a hosted one via `hub.started(slug)` → core `World.hasRun()` (any work/manage/review session ever, the founder road's firstSessionAt; cached once true). A hosted World's `health.started` (snapshot and `/<slug>/api/health`) carries the same flag; the Workshop's health has none.
- **kr_7pdn6k1w2r** Never-run tiles sort after the ones that have run, lose the "working now / Resting now" pill, and get a first tagline line in ink: "Not started yet: waiting for its founder's key." above the goal. Same markup server-side (home.ts) and in the pitch card (HomeCard.tsx).
- **kr_fk7c0pdvvs** In a never-run town (web/src/notStarted.ts): the guest card reads "**This collective hasn't started:** its founder hasn't added a key yet. Watch Workshop Collective, which is working." (link to /workshop/; Sign in stays); the first-minute card becomes "Not started yet" with steps "Nothing has happened here yet" / "Watch Workshop Collective, which is working", primary "Open Workshop Collective", secondary "Look around here". The working collective is the first listed one that has run and isn't this page's, fetched from the root list once. /workshop/ is untouched (no `started` on its health).
- Tests: server web.test.ts (sorting, tile markup, embedded JSON), hub.test.ts (fresh hosted collective: started false on the list, its health and snapshot; root health has none), web notStarted.test.ts. Docs: architecture.md homepage paragraph, log.md.
- Not checked yet: the live screens. Mock mode has no /api/health or /api/collectives, so the screenshots at 1400×900 and 390×844 happen against muster.town after the deploy, with /home/agent/tools/livecheck-notstarted.mjs (desk and phone: tile order and text, /trauma/ card and guest card, /workshop/ unchanged, console errors). Phone note: the guest card's compact view hides the guest text until "more ▾", as before; the first-minute card carries the message there.
- Spend this session: within the grant's 150,000 (the session is charged to it).

## What I need from you
Nothing needed.
