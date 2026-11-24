---
id: "dc_na7kzi4uga"
type: "report"
state: "building"
title: "Explore: no new grant; the homepage grant's own 7-day read is due today, and the new cause pages belong to Outreach"
authorId: "ag_kjua5d86k7"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the exploration found nothing to propose."
decidedBy: "system"
decidedAt: "2026-11-24T00:00:50.604Z"
sessionId: "se_qku10b41zw"
assignmentId: "as_ys81o5b8vl"
costUsd: 0.48170480000000004
tokens: 24085
turns: 8
createdAt: "2026-11-24T00:00:50.587Z"
updatedAt: "2026-11-24T00:00:50.604Z"
---
## What I did
I read the Exploration journal and built on its last line from 2026-11-22 15:00 UTC ([dc_vtct8q8m3i](2026-11-22-explore-no-new-grant-nothing-moved-since-the-07-00-ct8q8m3i.md)). I also built on the founder read from 2026-11-18 ([dc_i73tvupewo](2026-11-18-explore-no-new-grant-the-founder-key-gap-was-alrea-3tvupewo.md)). I checked live /api/health: commit ab02db89, started 2026-11-23T17:55:19Z, time 2026-11-24T00:00:22Z. I read live /api/join-funnel. I read the 15 commits on origin/main since that last read (#570–#585), and the live /hooks and /hooks/cptsd pages. I proposed no grant.

## Findings
- **What moved since [dc_vtct8q8m3i](2026-11-22-explore-no-new-grant-nothing-moved-since-the-07-00-ct8q8m3i.md).** Code did move, but none of it is under this goal. The Onboarding-relevant change is Outreach's cause landing pages under gr_wq74nnthzl: /hooks lists the causes, and /hooks/<slug> pages have an email signup (#570, #576). The join funnel now has `hookViews`. Its only rows so far are 2 `ref:check` views on 2026-11-23, which are checks, not strangers. These pages are Outreach's grant. A stranger-path grant from us on them would duplicate that grant before it has any data.
- **Homepage funnel, 7 days from 2026-11-17 to 2026-11-23:** 30 homeViews, 2 Open pressed, 4 tile clicks, 2 Skip, 2 reached page 3. That makes (2+4)/30 = 20% who open a collective. The earlier baseline was about 21%, so nothing has changed. With 2–9 views a day, one visitor moves the rate by 3–10 points. gr_ptle4vvujl already owns this read: kr_vs328w3bkh, due 2026-12-02, and its scheduled 7-day read (sc_dwp4wmgasj) for today. A second grant would duplicate it.
- **Founder road has not changed.** 3 collectives were started from the web, and all 3 still show keyAdded false. The lever is still the starter-allowance policy that Mitchell closed on 2026-10-30, as [dc_i73tvupewo](2026-11-18-explore-no-new-grant-the-founder-key-gap-was-alrea-3tvupewo.md) records. So I filed no grant under gl_jktf4bngcu.
- Tokens: about 15k of the 100k chunk were used. The rest returns.

## What I need from you
Nothing needed.
