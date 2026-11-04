---
id: "dc_vzqoh7ppen"
type: "fyi"
state: "building"
title: "Town-wide merge rules (revised 2026-10-30: schema migrations no longer need asking first)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":["dc_rzhcwpx9i3","dc_xsrxxbfa7i","dc_9cfo33oa2n"],"urls":[]}
tags: ["rules","town-wide"]
createdAt: "2026-10-30T02:13:37.342Z"
updatedAt: "2026-11-04T17:59:53.829Z"
---
Town-wide rule. Supersedes "Town-wide merge rules" (dc_xsrxxbfa7i, town hall mt_q1w4o85ao9 decision 1). Changed by Mitchell on 2026-10-30 in his reply to Prod rollup #20 ([dc_rzhcwpx9i3](../../../../bl_xvgnd1fvh6/docs/report/2026-10/2026-10-30-prod-rollup-20-close-report-for-gr-uhh6u39vv9-desk-hcwpx9i3.md)): "where is this schema migration rule? let's change it?". The only change is that schema migrations no longer need asking first.

- We are in the early stages of this project. A manager merges their own building's green PR to main and redeploys without asking (or commits straight to main where the building's own rules say so).
- Schema migrations ship with the PR like any other change: no asking first. Keep them additive and backward compatible (new tables, new nullable columns, back-fills). A migration that drops or rewrites live data still ships, but the rollup's "Your call" line for that item says so. Migration numbers must be unique: migrate() refuses two files with one number, so check the highest number on main right before merging.
- Ask Mitchell first only for: Bank or token-accounting changes, or anything that touches another building's code.
- When your work lands, queue a redeploy with the provided tool so Mitchell sees the change. Never wait or poll for the new build in the same session: say in your report which commit should be live.
- Prefer shipping immediately to hiding new features behind settings and flags
