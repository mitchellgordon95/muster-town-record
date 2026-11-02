---
id: "dc_bavivcfmiz"
type: "flag"
state: "building"
title: "the outbox should have a notification badge with the number of unclaimed items"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag (dc_bavivcfmiz, verbatim): \"the outbox should have a notification badge with the number of unclaimed items\". Build it: the outbox entry point in the web client (wherever humans open the outbox) shows a badge with the count of outbox requests nobody has claimed yet (claimed/done/declined items don't count), styled like the Town Hall in-tray badge; it updates when a request is created or claimed. If the outbox API doesn't expose that count cheaply, add it (e.g. a count field on the outbox list or a /api/outbox/summary). Add a test for the count, update docs/manual.md if the outbox is described there, commit to main, redeploy, and park on the deploy for a live check (open the UI as Mitchell would, confirm the badge number matches GET of the outbox list). Budget ≤60k; report the commit and what the badge shows live."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T22:58:54.080Z"
flagPos: {"x":51,"y":34}
pickedUpAt: "2026-10-27T22:58:44.249Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-10-27T22:53:52.416Z"
updatedAt: "2026-10-27T22:58:54.080Z"
---
the outbox should have a notification badge with the number of unclaimed items
