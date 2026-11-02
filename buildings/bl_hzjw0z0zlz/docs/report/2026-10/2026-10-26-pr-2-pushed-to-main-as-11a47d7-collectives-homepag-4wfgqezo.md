---
id: "dc_zm4wfgqezo"
type: "report"
state: "building"
title: "PR 2 pushed to main as 11a47d7: collectives homepage at / (Workshop + \"Coming soon\" placeholder) and /api/collectives from collectives/registry.json; redeploy queued, live check parked"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR 2 (11a47d7) approved: homepage at /, registry, /api/collectives, hash forwarding, 6 tests, docs. Your parked continuation does the live check once 11a47d7 is live; keep the query-302 decision but note it in the live-check report so Mitchell can overrule."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T16:35:39.660Z"
sessionId: "se_x9wqqha05h"
assignmentId: "as_6rto5vh0i3"
costUsd: 1.3967147000000004
tokens: 86399
turns: 40
createdAt: "2026-10-26T16:35:09.814Z"
updatedAt: "2026-10-26T16:35:39.660Z"
---
## What I did
I built PR 2 of gr_cm3zha6mk6 from my scoping note [dc_wgpjthaes2](../../note/2026-10/2026-10-26-scoping-note-for-gr-cm3zha6mk6-pr-1-2-move-the-wor-pjthaes2.md) and pushed it straight to main as **11a47d7**, rebased on 6130c4e. I queued a redeploy. The live check is parked until 11a47d7 is live.

## Findings
- **`GET /`** is now a server-rendered HTML page from the new `packages/server/src/home.ts`. It needs no JS and no SPA.
  - One plain sentence says what Muster Town is, then two cards follow.
  - **Workshop Collective** shows its tagline and goal, plus an "Open Workshop Collective →" button that links to `/workshop/`.
  - **"Your collective here"** has a dashed border, a "Coming soon" pill and no link.
  - The footer links to the README and to `/api/collectives`.
  - I screenshotted it locally at 1400×900 and 390×844, and both read cleanly. After the first look I shortened the placeholder text, because it said "Coming soon" twice.
- **Registry:** the list lives in `collectives/registry.json`, validated by `CollectiveRegistry` in the schema.
  - The file is read on every request, so an edit shows up without a restart.
  - The entry whose url is `/workshop/` takes its name, tagline and goal from the live town row.
  - If the file is missing or invalid, the page lists only this server's own collective.
- **`GET /api/collectives`** returns `{collectives: [...]}`, the same list the page shows.
- **Hash links:** an inline script in `<head>` sends `/#/doc|grant/…` to `/workshop/#/…` before the page renders, so old links still open the doc or grant.
- **Query decision:** `/` with any query still 302s to `/workshop/` and keeps the query.
  - Why: the homepage takes no parameters, and every existing query link (`/?guest`, `?as=visitor`) is meant for the client.
  - A bare `/` shows the homepage.
- **Tests:** server `test/web.test.ts` has 6 tests covering:
  - the homepage HTML, its no-cache header and the forwarding script
  - the query 302s
  - the live-row overlay
  - HTML escaping
  - one Open link only (the placeholder has none)
  - the fallback for a missing or invalid registry
  - that the checked-in registry parses
- **Test runs:** `npm run typecheck` and the full vitest suites all passed: server 73/73, core 265/265, runtime 119/119. After the rebase I re-ran the server typecheck and web.test.ts, and both passed.
- I updated `docs/architecture.md`, the README (the client/homepage sentence and the layout line) and `docs/log.md`. I did not touch the sign-in flows (those are PR 3).
- **Should be live after the redeploy:** 11a47d7. The live check (two cards, Open → /workshop/ read-only, /#/doc/<real id> → doc, /?guest 302s, plus a homepage screenshot) runs on resume.

## What I need from you
Nothing needed.
