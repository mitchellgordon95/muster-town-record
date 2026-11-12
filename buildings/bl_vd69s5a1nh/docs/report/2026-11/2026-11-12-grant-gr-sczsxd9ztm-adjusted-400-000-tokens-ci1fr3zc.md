---
id: "dc_ifci1fr3zc"
type: "report"
state: "building"
title: "Grant gr_sczsxd9ztm adjusted: 400,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:149581:bl_vd69s5a1nh"]
decision: "approve"
decisionNote: "Taken in. Mitchell adjusted gr_sczsxd9ztm from 120k to 400k (147,188 spent), which released the held step as_q4ajtv45dh: Mara 1 is running it now. The 400k means he wants kr_0xk1ex7tus reached (tests ≤110 s, total ≤140 s on CI), not the grant closed with it missed, so I told the fork to finish the 10-run read and then profile the core test files per file for the lever, and I queued the PR step behind it."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-12T14:41:21.149Z"
createdAt: "2026-11-12T14:40:33.937Z"
updatedAt: "2026-11-12T14:41:21.149Z"
---
Written by the town: Mitchell adjusted grant gr_sczsxd9ztm at its checkpoint (event 149581, 2026-11-12 14:40 UTC).

## Summary

Grant gr_sczsxd9ztm "Bring the CI check back under 3 minutes" adjusted by Mitchell: 400,000 tokens.

Status funded; 147,188 of 400,000 tokens spent; key results kr_9xqxj8v5cl [claimed] PR #247 (test DBs start from one schema image instead of replaying all 96 migrations) is merged to main and live on muster.town; kr_0xk1ex7tus [at-risk] Over the 10 green main CI runs after the grant's last merge, the `check:` line's median is tests ≤110 s and total ≤140 s (down from 158 s / 180 s on 2026-11-06).

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
