---
id: "dc_qda224cdci"
type: "report"
state: "building"
title: "Join approval shows live to the requester (flag dc_1kylouq1l7 nit 2): 473f871 merged, redeploy queued, live check parked"
authorId: "ag_927uzfsbdl"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Nit 2 of flag dc_1kylouq1l7: PR #97 = 473f871, web-only, no migration or Bank change; requester refetches /api/auth/me on the access-decision event and toasts. Live check already parked (as_e96g5uwls1 on deploy 473f871). Folds into rollup 31 as Shipped with nit 1 (as_wcq5obyz4g); Your call = Mitchell + friend re-run the join once live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T23:24:23.495Z"
sessionId: "se_dk8y0ipgs1"
assignmentId: "as_eljhzw663q"
costUsd: 0.8549473999999999
tokens: 42747
turns: 26
createdAt: "2026-10-29T23:24:11.729Z"
updatedAt: "2026-10-29T23:24:23.495Z"
---
## What I did
Traced the join flow: Ask to join (hud.tsx AskToJoin → POST /api/access-requests) → admin decides in the Town Hall in-tray (POST /api/access-requests/:id/decide → core `decideAccess`). Fixed the requester's page so it no longer needs a refresh. [PR #97](https://github.com/mitchellgordon95/muster-town/pull/97), CI green, merged as **473f871**. Redeploy queued. This code is the join flow, which may be Onboarding's area; Mitchell planted this flag in the Workshop, and that is my authorization.

## Findings
- **Cause:** the server side already worked. `decideAccess` grants the `member` role and appends a `system` event `{accessRequestId, userId, granted}`. Every WebSocket gets that event. Permissions are checked again on each WS message and REST call, so the requester could already act once let in. But the web client reads `me` (`canInteract`, `accessRequest`) only at page load and ignored the event. So the guest card kept saying "Asked." until a reload.
- **Fix (web only, no migration, no Bank change):**
  - `state.ts` adds `isMyAccessDecision(e, myUserId)`. It runs on live events and on the event refetch after a reconnect, and it calls a new `store.onAccessDecided` hook.
  - `app.tsx` points that hook at a refetch of `/api/auth/me`. The guest card then turns into the member HUD, and walking, talking and Connect your agent are enabled.
  - A toast appears only when something actually changed. Let in: "You're in: an admin let you join…" (ok). Declined: "Your request to join was declined this time. You can ask again tomorrow." (info). Declining is covered too.
- **Tests:**
  - New `packages/web/test/accessDecision.test.ts` has 3 tests, all passing. It checks that only a decision on my own request triggers the refetch (the ask itself and other people's decisions don't), that both the socket path and the reconnect path trigger it, and the toast rules.
  - Full `npm run typecheck` is green and CI on PR #97 passed.
- **Not yet verified live:**
  - No screenshot: the change is a state transition, and capturing it needs two signed-in humans.
  - The parked check will only confirm the live commit and that the new strings are in the live bundle. The real end-to-end test needs Mitchell and his friend to do it again: the friend approves, and Mitchell's open page should switch to the member view with the "You're in" toast, with no refresh.

## What I need from you
Nothing needed now. After 473f871 is live, Mitchell and his friend can re-run their join to confirm it end to end.
