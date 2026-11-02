---
id: "dc_r3k8vozh1q"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-27 06:10Z: operating manual live in the Town Hall (dc_irk1w62mpv, opened from \"?\"), verified claim by claim; first staleness sweep done for KR 6; gr_rdyrjzclfe still awaits your decision"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_mkvyq5rc2b","dc_obzzxrdxwr","dc_6h20dbo4fu","dc_3r5ypcdqip","dc_dy4dwf5jw5","dc_4behnnnglt","dc_f3sgfhesfe","dc_qr00e8k1yk","dc_j30thna89z","dc_qipzno7p8u","dc_krsyw903ih","dc_qh89ud44pi"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Onboarding: gr_rdyrjzclfe (hosted collectives at muster.town/<name>, 1,000,000 adjusted tokens) is funded by Mitchell. Terms: anyone signed in may start a colle"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:43:04.341Z"
sessionId: "se_pp2aiehoo4"
createdAt: "2026-10-27T05:51:39.713Z"
updatedAt: "2026-10-27T17:43:04.341Z"
---
## Shipped
- **Operating manual, live on muster.town** as library doc [dc_irk1w62mpv](../../../../../library/article/2026-10/2026-10-27-operating-manual-k1w62mpv.md) (Town Hall, tagged manual): 9 sections, opened from the HUD "?" or `/#/manual/<section>`. Your ask from [dc_jrvx5amnj6](2026-10-26-onboarding-rollup-2026-10-26-22-35z-permissions-re-vx5amnj6.md) (manual for humans in the Town Hall, "?" opens it; repo stays for agents). Commits bb7c00f (sheet + docs/manual.md, Craig [dc_qr00e8k1yk](2026-10-27-operating-manual-edition-1-on-main-as-bb7c00f-the-00e8k1yk.md)), 2d23468 (seed + GET /api/manual, [dc_j30thna89z](2026-10-27-operating-manual-server-half-on-main-as-2d23468-se-0thna89z.md)), 8a7a7ca (edition 2, [dc_3r5ypcdqip](2026-10-27-operating-manual-edition-2-on-main-as-8a7a7ca-tae-5ypcdqip.md)). Live body = edition 2; Tae's live check [dc_mkvyq5rc2b](2026-10-27-manual-edition-2-live-check-all-9-rows-pass-6-rewr-vyq5rc2b.md): all 9 rewritten claims pass against the live code for a let-in member.
- **How the manual stays current:** docs/manual.md in the repo is the source; on boot the server replaces the live doc only if its body still equals a past repo edition (sha256 list `PAST_MANUAL_EDITIONS`). A hand edit in the UI is never overwritten, but also stops getting upgrades.
- **Staleness sweep 1 (KR 6)**, Craig [dc_obzzxrdxwr](2026-10-27-onboarding-staleness-sweep-1-10-materials-checked-zzxrdxwr.md), commit 00a6223 on main: 10 onboarding materials inventoried against 88 commits since 10-25; 7 stale claims and 3 gaps fixed (manual edition 3: media paste, @mention wakes, outbox answers reach the asker; README, AGENTS.md, CLAUDE.md drift). Skill onboarding-staleness-sweep [dc_0bfvvjyif1](../../skill/2026-10/2026-10-27-onboarding-staleness-sweep-fvvjyif1.md) for the daily run (≈30 k tokens quiet day, 60–90 k busy). Redeploy queued; 00a6223 not live yet at 05:49Z (live: 07f7957).
- Style guide skill [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md) updated for the manual sheet ([dc_dy4dwf5jw5](2026-10-27-style-guide-skill-dc-q736158pnn-updated-for-the-op-4dwf5jw5.md)).

## Decided
- [dc_mkvyq5rc2b](2026-10-27-manual-edition-2-live-check-all-9-rows-pass-6-rewr-vyq5rc2b.md) (Tae, edition 2 live check, all pass, 70 k) → approve. One wording nit (reviewers see Call meeting only with meeting.facilitate) goes into the next manual edit via Craig.
- [dc_obzzxrdxwr](2026-10-27-onboarding-staleness-sweep-1-10-materials-checked-zzxrdxwr.md) (Craig, sweep 1, 85 k) → approve; assigned Craig a ≤40 k live check of edition 3 (waitFor deploy 00a6223) and sweep 2 (after 2026-10-28T05:45Z, ≤100 k), both exploration on kr_hee2pa2d5r.
- [dc_6h20dbo4fu](2026-10-27-key-result-kr-hee2pa2d5r-written-by-mitchell-20dbo4fu.md) (notice: you wrote kr_hee2pa2d5r) → approve; sweep 1 assigned from it.
- [dc_3r5ypcdqip](2026-10-27-operating-manual-edition-2-on-main-as-8a7a7ca-tae-5ypcdqip.md) (Craig, edition 2, 55 k) → approve; Tae's live check assigned.
- [dc_4behnnnglt](2026-10-27-manual-edition-1-live-check-the-sheet-passes-5-cla-ehnnnglt.md) (Tae, edition 1 claim check: 6 wrong claims, 3 gaps, 73 k) and [dc_f3sgfhesfe](2026-10-27-operating-manual-live-check-on-muster-town-all-che-sgfhesfe.md) (Craig, technical check, 19 k) → approve; edition 2 assigned to Craig.
- [dc_qr00e8k1yk](2026-10-27-operating-manual-edition-1-on-main-as-bb7c00f-the-00e8k1yk.md) (Craig, edition 1 build, ≈169 k) and [dc_j30thna89z](2026-10-27-operating-manual-server-half-on-main-as-2d23468-se-0thna89z.md) (server half, parked) → approve; live checks assigned.
- [dc_dy4dwf5jw5](2026-10-27-style-guide-skill-dc-q736158pnn-updated-for-the-op-4dwf5jw5.md) (my style-guide update) → approve.
- [dc_qh89ud44pi](2026-10-27-session-ended-without-a-report-operating-manual-fo-89ud44pi.md) (build died at desk start, 0 tokens) → redirect to a retry. [dc_krsyw903ih](2026-10-27-manual-live-check-not-run-craig-s-manual-session-d-syw903ih.md), [dc_qipzno7p8u](2026-10-27-manual-live-check-not-run-again-only-craig-s-serve-pzno7p8u.md) (Tae's checks that started before the deploy and stopped themselves, 8 k) → approve.

## Key results
- No funded grant. Open proposal gr_rdyrjzclfe for kr_7316be4jqw (hosted collectives at muster.town/<name>, 1,000,000 adjusted tokens), proposed 04:10Z, waiting on you.
- kr_hee2pa2d5r (staleness < 24 h): on-track; sweep 1 done, sweep 2 queued for tomorrow 05:45Z. Each day's sweep report is the "merge report" the KR asks for and will appear under Shipped.
- kr_1rpq0738sw, kr_z0mj5teeu7: on-track, nothing new this period. kr_tzg9en02dh: cut in meeting mt_rjhwj2qggm, still listed; delete when convenient.
- Spend today by lane: exploration 131,213 / 828,571 tokens; directed 516,299 tokens (the manual work traces to your reply on [dc_jrvx5amnj6](2026-10-26-onboarding-rollup-2026-10-26-22-35z-permissions-re-vx5amnj6.md)).

## Needs from Mitchell
1. Read the manual (press "?" on muster.town, or [dc_irk1w62mpv](../../../../../library/article/2026-10/2026-10-27-operating-manual-k1w62mpv.md)) and reply with what is missing or wrong. If you want to edit it by hand in the UI, say so: a hand edit is kept forever but the repo stops upgrading it, so edits should then go through docs/manual.md instead.
2. Decide gr_rdyrjzclfe (fund, counter or reject) so hosted-collective work can start; Tae is idle.
