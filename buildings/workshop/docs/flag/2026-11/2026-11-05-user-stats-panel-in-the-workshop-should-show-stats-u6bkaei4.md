---
id: "dc_r7u6bkaei4"
type: "flag"
state: "building"
title: "user stats panel in the workshop should show stats for community engagement in this specific collective (hosted), not m…"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_r7u6bkaei4, piece 1 of 3 (the other two are separate assignments): \"user stats panel in the workshop should show stats for community engagement in this specific collective (hosted), not muster town in general\".\n\nContext: the User stats stand in the Town Hall opens packages/web/src/panels/StatsPanel.tsx, which renders GET /api/join-funnel (packages/server/src/app.ts:213-220: a hosted collective, prefix set, returns only its own world's counts; the root sums every hosted one and adds founder roads). The columns (StatsPanel.tsx:18-28) are the Muster Town join funnel: Home, Saw card, Visitors, Pressed Sign in, Signed in, Asked, Let in, Declined, Acted. For a hosted collective (e.g. /workshop/) most of those are Muster-Town-wide ideas (homepage views are only counted at the root, app.ts:208) and tell a collective's captain nothing about engagement in their own collective.\n\nDo: (1) Open the live hosted panel (https://muster.town/workshop/ → Town Hall → User stats stand; curl GET https://muster.town/workshop/api/join-funnel and the root's) and record exactly what it shows today, and whether any number there is really the root's (check the client's API_BASE path and the server's prefix handling). (2) Redesign the hosted collective's panel to show community engagement in this collective: counts only, never who, last 30 days, by day: e.g. members let in, humans who visited (sessions seen), says/tells by humans, 1:1s opened with managers, flags planted, reports/rollups read or decided, grants proposed/funded by members, meetings attended by humans; derive from the event log and existing tables; pick the 6-9 columns that a captain of a hosted collective would actually read, keep the join steps that are the collective's own (Asked, Let in, Declined, Acted). The root (muster.town) panel keeps the Muster-Town-wide funnel plus the per-collective table. (3) Ship it: server endpoint (new or extended, e.g. GET <prefix>/api/engagement or extra fields on /api/join-funnel), the panel, tests (packages/web/test/statsPanel.test.tsx), docs/manual.md line. Merge your green PR; do not call redeploy (CI promotes main); report the commit and what a human sees on https://muster.town/workshop/ afterwards, with a cropped screenshot."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T19:16:42.783Z"
flagPos: {"x":75,"y":10}
pickedUpAt: "2026-11-05T19:15:48.284Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-11-05T19:15:35.015Z"
updatedAt: "2026-11-05T19:16:42.783Z"
---
user stats panel in the workshop should show stats for community engagement in this specific collective (hosted), not muster town in general

also can we get planner to stand next to the goals and secretary to stand next to the intray when they're not doing anything, they're just lingering by the mod table

also why is the mod table ban tab and the outbox in the same group? those should be separate right?
