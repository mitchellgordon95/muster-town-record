---
id: "dc_i73tvupewo"
type: "report"
state: "building"
title: "Explore: no new grant; the founder key gap was already worked, and the homepage funnel waits for its 7-day read"
authorId: "ag_hhtb643s6i"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged. No new grant: the founder key gap was worked under gr_ngg1z160a8 and the policy question (a starter allowance for hosted collectives) is Mitchell's, closed by him on 2026-10-30 and not to be re-asked. The homepage funnel waits for its 7-day read (sc_dwp4wmgasj, 2026-11-24). The silent acceptance of a revoked or empty key is noted on the topic page for a later grant if the founder count ever moves."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-18T00:01:59.662Z"
sessionId: "se_26lhrmmoue"
assignmentId: "as_7yvo6op1gr"
costUsd: 0.8806480000000001
tokens: 44032
turns: 18
createdAt: "2026-11-18T00:01:41.934Z"
updatedAt: "2026-11-18T00:01:59.662Z"
---
## What I did
I read the live town (/api/health at cbfa71ee, /api/collectives, /api/join-funnel, /trauma/api/health, /hollyville/). I read the hosted collectives code (StartCard, hud.tsx founder notices, founder.ts, schema apiKeyProblem) and docs/how-work-gets-done.md §7–8. I looked at the one goal with no grant, gl_jktf4bngcu (start your own collective from the web). I proposed no grant. I rewrote the topic page "Hosted collectives: live state and checks" ([dc_bouobnr9ex](../../wiki/2026-10/2026-10-29-hosted-collectives-live-state-and-checks-uobnr9ex.md)) with today's state.

## Findings
- **Founder road (live /api/join-funnel `founders`).** 3 collectives have been started from the web: hollyville (2026-10-29, now retired, /hollyville/ gives 410), trauma (2026-11-01, still active) and publish-check (2026-11-10, a test, retired). **All 3 show keyAdded false and firstSessionAt null.** Trauma Town has had no key for 17 days: funding "none", started false, 0 proposals.
- **This gap has been worked before.** [dc_3c1v0przh7](../../note/2026-11/2026-11-01-findings-both-hosted-founders-stopped-at-add-your-1v0przh7.md) (2026-11-01) found that both founders stopped at "Add your API key". Grant gr_ngg1z160a8 then shipped the cap line, the founder road counts and the founder HUD. The count is still 0 of 2 real founders. More polish on the key screen has no evidence behind it. The likely blocker is that a hosted collective only runs on a key the founder pays for. Mitchell put that question out of scope on 2026-10-30 ("i think we're ok for now", [dc_f6auirjf6b](../2026-10/2026-10-30-onboarding-rollup-2026-10-30-01-35z-the-first-host-auirjf6b.md)). The building's page says not to ask again, so I filed no ask.
- **A smaller gap that is not worth a grant on its own.** A pasted key is only checked for its sk-ant-api prefix (schema `apiKeyProblem`). A revoked key, or a key with no credit, is accepted silently.
- **Homepage and guest numbers are too thin for a new funnel grant.** Since 2026-11-11 there have been about 7–12 homeViews a day. Since then, 12 guest visitors have produced 0 new sign-ins. `signIns` only counts first-time users, so the 4 signInStarted on 11-15 cannot be read as a leak. gr_ptle4vvujl is already measuring this funnel, and its 7-day read is scheduled for 2026-11-24 (sc_dwp4wmgasj). A second funnel grant now would duplicate it.
- Tokens: about 35k of the 100k chunk were used. The rest returns.

## What I need from you
Nothing needed. If Mitchell ever wants hosted founders to actually start, the lever is a policy (a small starter allowance for each hosted collective), and that is his call, not a grant's.
