---
id: "dc_57nuw740sc"
type: "fyi"
state: "building"
title: "Merge rules for Bank Transparency (revised 2026-10-30: schema migrations no longer need asking first)"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_vzqoh7ppen","dc_rzhcwpx9i3","mt_q1w4o85ao9"],"urls":[]}
tags: ["rules","merge","deploy"]
createdAt: "2026-10-27T22:34:56.595Z"
updatedAt: "2026-10-30T02:14:33.497Z"
---
Standing rules for every session in the Bank Transparency. Copy of the town-wide rule [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-10-30-schema-mi-qoh7ppen.md) (revised by Mitchell on 2026-10-30 in his reply to Prod rollup #20, [dc_rzhcwpx9i3](../../../../bl_xvgnd1fvh6/docs/report/2026-10/2026-10-30-prod-rollup-20-close-report-for-gr-uhh6u39vv9-desk-hcwpx9i3.md); supersedes dc_xsrxxbfa7i / town hall mt_q1w4o85ao9). The only change from the 2026-10-27 version: schema migrations no longer need asking first.

- We are in the early stages of this project. The manager and the manager's forks commit green work straight to main (rebase on origin/main first); CI redeploys on every green push. A visitor commits on a branch and opens a draft PR; the manager merges it once checks are green.
- Schema migrations ship with the change like anything else: no asking first. Keep them additive and backward compatible (new tables, new nullable columns, back-fills). A migration that drops or rewrites live data still ships, but the rollup's "Your call" line for that item says so. Migration numbers must be unique (migrate() refuses two files with one number): check the highest number on main right before merging.
- Ask Mitchell first only for: Bank or token-accounting changes, or anything that touches another building's code. Everything else: merge, then say in your report which commit should be live.
- After your work lands, queue a redeploy with the `redeploy` tool if CI hasn't (the desk image needs `redeploy image=true`); never wait or poll for the new build in the same session. Park with `submit_report resumeWhen {deploy: "<sha>"}` and verify live next session.
- Never force-push or rewrite history. Put the commit sha (or PR URL) in your report.
