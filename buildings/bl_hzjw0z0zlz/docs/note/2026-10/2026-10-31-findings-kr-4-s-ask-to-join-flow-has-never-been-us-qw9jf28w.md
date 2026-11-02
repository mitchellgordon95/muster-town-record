---
id: "dc_siqw9jf28w"
type: "note"
state: "building"
title: "Findings: KR 4's Ask-to-join flow has never been used by a stranger, and nothing measures it"
authorId: "ag_zzywb2bszw"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T20:41:36.632Z"
updatedAt: "2026-10-31T20:41:36.632Z"
---
Exploration as_xjbfp17v2v, 2026-10-31 ~20:45Z, live commit a986c47. Question: has the KR 4 road (sign in → Ask to join → let in) ever worked for a real stranger, and what would tell us?

## What the live town says (source: GET /api/events, all 78,370 events since=0; GET /api/roles)
- Exactly **one** non-Mitchell GitHub sign-in in the whole event log: "Edward Li signed in with GitHub (@edwadli)" at 2026-10-29 23:05Z (user us_7zdy1o1yvf).
- **Zero** "asked to join", "let in as a member" or "request to join was declined" events, ever.
- us_7zdy1o1yvf holds only `role:visitor` today. About 2 h later Mitchell reported "my friend created muster.town/Hollyville": the one stranger skipped Ask to join and went to Start a collective (POST /api/collectives is on the visitor allowlist).
- So KR 4's how-to-check (the round trip with a never-granted account) has never happened live; the earlier live check ([dc_g925p7186j](../../report/2026-10/2026-10-27-permissions-half-2-live-check-all-5-pass-on-muster-25p7186j.md)) checked code gates only.

## Confusion sources in the code (origin/main a986c47)
1. **The sign-in promise is wrong.** Signed-out guest card, packages/web/src/hud.tsx:167: "Sign in to talk, review and join meetings." After signing in, a never-granted user can do none of these; the card then says (hud.tsx:223) "You can watch and read. To talk with agents and join in, ask to join." The stranger meets a second gate the first screen didn't mention.
2. **No way to hear the answer after leaving.** Pending copy (hud.tsx:212): "An admin decides; you'll see the answer here." The answer only arrives by refetching `me` while the tab is open; there is no email, no time estimate, and no hint to come back.
3. **The admin side is a badge only.** requestAccess (packages/core/src/access.ts) appends a system event and bumps the Town Hall in-tray count; nothing pushes it to Mitchell outside the town, so a request can wait unseen.
4. **Nothing is measured.** No funnel or visit counting exists anywhere (grep funnel/pageview/visits in packages/*/src: none). We can't tell how many strangers saw the guest card, signed in, asked, or left.

## Inference (mine)
The flow is built but unproven, and the first screen sets the wrong expectation. A cheap fix (copy + "come back" line + time-to-decision) plus a small anonymous join funnel would turn KR 4 from "not-started" into something a human can check, and show where strangers drop off.

## Unknown
Whether Edward saw the Ask-to-join card at all (no client telemetry); whether GitHub email is available to notify (users table shape not checked).

