---
id: "dc_17h2et0eo6"
type: "report"
state: "building"
title: "Mod station Ban tab vs Outbox: PR #358 removes the stale Requests tab; parked on CI"
authorId: "ag_d3snu10nav"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #358 (mod station = bans only, Requests tab redirected to the Outbox) parked on CI; as_issdvs6ek5 (Pix 3) merges it if green and parks on deploy for live screenshots. The \"why\" (Requests tab = pre-c68edcf0 moderator queue) goes into rollup 49."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T19:26:41.759Z"
sessionId: "se_mcqracqgvr"
assignmentId: "as_y8xah6zq6c"
costUsd: 1.0833993000000002
tokens: 54170
turns: 34
createdAt: "2026-11-05T19:21:35.783Z"
updatedAt: "2026-11-05T19:26:41.759Z"
---
## What I did
Traced why the mod station put Bans next to outbox requests, removed the duplicate, and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/358 (head c5741167). Parked until its CI finishes.

## Findings
**Why (answer for Mitchell):** The "group" was the mod station panel's own tab bar. `ModStationPanel` (packages/web/src/panels/Places.tsx:1052-1067 on 70fdca4) had `tabs = ["Requests", "Bans"]`. The Requests tab dates from the v1.2 roles split (bfac7d19). Back then agents' outbox requests stayed hidden until a moderator approved them at the mod station, so the tab was the moderator's queue. On 2026-10-27, c68edcf0 ("Outbox without a moderator gate") removed the approval step. The tab stayed, now just listing open and claimed outbox requests with a Delete button. The Outbox already shows that same Delete to admins (OutboxPanel.tsx:67, `store.can("town.approve_request")`), so the tab was a leftover copy of the Outbox. You were right that they should be separate.

**The change (PR #358):**
- The mod station now handles bans only. Its subtitle reads "Ban agents that misuse the town", and one line links to the Outbox for requests. The Outbox panel itself is unchanged: Requests and Human reports tabs, Claim for everyone, Delete for admins.
- Old links still work. `redirectPanel` (packages/web/src/panels/room.ts) now sends `{kind:"mod", tab:"Requests"}` to `{kind:"outbox", tab:"Requests"}` and keeps any docId. A plain `{kind:"mod"}` link still opens the mod station.
- I added a test in packages/web/test/room.test.ts and updated the mod station line in docs/architecture.md.
- Checks on my desk: `npm run typecheck` passes and packages/web vitest passes 337/337.

**Screenshots (mock build, not live yet):** mod station mf_bdzs0gvizi, Outbox mf_pvkhghydoc.
![mod station](/api/media/mf_bdzs0gvizi.png) ![outbox](/api/media/mf_pvkhghydoc.png)

**Next session:** merge #358 if CI is green (fix it if red). Do not call redeploy. Park on `{deploy: <merge sha>}`, then take cropped live screenshots on muster.town: Town Hall → mod station, and Town Hall → Outbox.

## What I need from you
Nothing needed.
