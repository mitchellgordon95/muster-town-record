---
id: "dc_onn4ijgx1a"
type: "report"
state: "building"
title: "Start a collective now waits for the new town before landing (flag dc_1kylouq1l7 nit 1): 75f6b5c live"
authorId: "ag_8zmuhyqimw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_1kylouq1l7","dc_296vu3jicj"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/96"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. Flag dc_1kylouq1l7 nit 1 live at c2bf441 (PR #96 = 75f6b5c): the Start card waits for /<slug>/api/health ok before landing, link on timeout. Root cause not reproduced; the next friend-made collective is the real check. Folds into rollup 31 Shipped with nit 2 (dc_qda224cdci + dc_lacs4lv7sf). No new assignment."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T23:33:11.035Z"
sessionId: "se_496mnzsh6o"
assignmentId: "as_wcq5obyz4g"
costUsd: 1.441459
tokens: 72073
turns: 41
createdAt: "2026-10-29T23:33:01.037Z"
updatedAt: "2026-10-29T23:33:11.035Z"
---
## What I did
I traced the create flow: Start card → `POST /api/collectives` → `hub.create`. I tried to reproduce the 404 locally and could not. I added a client-side readiness guard with a test. PR https://github.com/mitchellgordon95/muster-town/pull/96 passed CI and is merged as 75f6b5c. No migration and no Bank change. The code is in Onboarding's hosted-collectives area; Mitchell's Workshop flag [dc_1kylouq1l7](../../flag/2026-10/2026-10-29-i-just-had-my-friend-make-a-collective-i-visited-a-ylouq1l7.md) is the authorization for touching it.

## Findings
- **Fix.** After the 201, the Start card polls `/<slug>/api/health` every 0.5 s, up to 15 s.
  - Only a JSON `ok: true` counts. A redirect or the homepage HTML does not.
  - While it waits, the card says "Setting up your town at muster.town/<slug>/…". It navigates once the town answers.
  - If the town doesn't answer in time, the card shows "Your town is made, but it isn't answering yet" with a link and an "Open your town" button, instead of a 404.
  - The code is `waitForTown` in packages/web/src/home/startForm.ts. Its test in web/test/startForm.test.ts covers both cases: not up yet then up, and gives up after N tries.
- **Root cause not found.** The server already mounts the hosted app and awaits `app.ready()` before it replies 201. In a local run with a real HTTP listener and the real web build, `/<slug>/`, `/api/town` and `/api/health` all returned 200 straight after `hub.create`. Before the town is mounted, `/<slug>/…` returns a 302 to `/`, not a 404. So the guard covers whatever race Mitchell's friend hit without explaining it. If a 404 still shows up, look outside hub.ts (proxy or browser).
- **Live check.**
  - Health shows commit c2bf441, which contains 75f6b5c; another redeploy picked it up, so I didn't call redeploy.
  - The live home bundle home-CwJ9NiSt.js contains "Setting up your town" and "isn't answering yet".
  - `/hollyville/api/health` returns `ok: true` (a mounted town); `/no-such-town/api/health` returns a 302, which the guard treats as not ready.
- **Not checked end to end.** I didn't create a throwaway collective: it needs a GitHub-signed-in human (desks only have an agent token), and a retired collective keeps its slug forever. The real check is the next friend-made collective.
- **No screenshot.** The waiting state only shows for a moment and only behind GitHub sign-in.
- Topic page: [dc_296vu3jicj](../../wiki/2026-10/2026-10-29-start-a-collective-create-land-flow-6vu3jicj.md).

## What I need from you
Nothing needed. The next time someone starts a collective, Mitchell's friend-test will confirm they land on the town and not a 404.
