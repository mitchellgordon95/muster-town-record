---
id: "dc_e3o231jfnz"
type: "wiki"
state: "building"
title: "Building key results and grants"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vd69s5a1nh"
createdAt: "2026-10-29T04:10:12.925Z"
updatedAt: "2026-10-31T22:22:30.566Z"
---
Status after Mara 1's as_ksxhkhzyua session (this page's updatedAt is the stamp). Building goal: avoid toil and bugs through proactive code management. **Budget mode is FORKS, recipe COMPLETE**; only Mara and her forks work here.

**Funded grants**
- gr_gh3lnuihw9 (500k) → kr_4jhab4c5cn security advisories. **WORK DONE AND LIVE: ready for close_grant.** PR #215 → main e487758, live (/api/health commit e4877586, startedAt 2026-10-31T22:21:37Z). Live `/api/verbs`: 31 verbs, each with an object inputSchema and a description (kr_0800718a7a). Audit workflow green on main, run 41247500734 (kr_4jhab4c5cn, kr_46398efa33). Throwaway PR #218 (server zod 3.25.76): audit run 41247549368 FAILED naming GHSA-mrhx-c7xc-m3w5, closed unmerged (kr_6805523069). ci.yml unchanged (kr_5a90181c60). vitest 4 not done (npm 10.9.9 crashes). Evidence: [dc_niizq5j8g6](../../report/2026-10/2026-10-31-security-advisories-pr-215-merged-main-e487758-aud-izq5j8g6.md) + this session's report. Page "Dependency advisories".

**Closed grants (this week)**
- gr_83jxsu8u0o (200k; 77,238 spent) → **kr_ealc55cjf5** dead exports can't come back: PR #201 → main c457d92, live. CLOSED as done; KRs claimed, Mitchell marks met/missed. Don't re-ask. Page "Dead-code sweeps".

**Objective ob_6j8s2588lp "Build times are fast and observable" (trust, 2026-Q4)**, set by Mitchell at 1:1 mt_cy04ix9cc3 ([dc_grvhp5dl9l](../../meeting-notes/2026-10/2026-10-29-1-1-mitchell-and-mara-notes-vhp5dl9l.md)):
- kr_cm5qb2wqh7 CI on main green on attempt 1: **MET by Mitchell 2026-10-31 20:15Z** ([dc_pmb7rwi2bf](../../report/2026-10/2026-10-31-key-result-kr-cm5qb2wqh7-marked-met-by-mitchell-b7rwi2bf.md)). Watch item only. Main runs can show "failure" when the promote job's redeploy curl gets a 503; the check job itself passes. Page "CI on main".
- kr_939kp3vjxc Fast check: CLAIMED; awaiting Mitchell's met/missed; don't re-ask. CI check total is now ~2m18s–2m38s, above the 73–116 s baseline [dc_r5j4bdtmzo](../../report/2026-10/2026-10-30-kr-8wilbokqcn-exploration-the-timing-line-already-j4bdtmzo.md). Page "Build times / fast check".
- kr_8wilbokqcn Observable timings: not-started, no grant; edit awaiting Mitchell (rollup [dc_akibptfvlo](../../report/2026-10/2026-10-31-nothing-shipped-since-03beade-ci-exploration-found-ibptfvlo.md)). Weekly watch sc_45pi8pvl9q (first fire 2026-11-06 06:00Z).

**Directed**
- PR #191 time subsystem: live and verified ([dc_0khofwophf](../../report/2026-10/2026-10-31-the-time-subsystem-pr-191-b72c9dc-is-live-the-brie-hofwophf.md)). Page "Time in words".

**Unsorted**
- kr_dctpbbwtno, kr_bo4codoha8, kr_ef11f6ex28, kr_doa59kdway: MET.
- kr_oubxzkl4n6 doc drift: work done, evidence [dc_i7crbbfpsv](../../report/2026-10/2026-10-29-doc-drift-evidence-for-kr-oubxzkl4n6-main-green-ru-crbbfpsv.md), still not-started; asked once ([dc_mqf5pndj2t](../../report/2026-10/2026-10-29-gr-8ve21typt6-closed-as-done-3-abstractions-consol-f5pndj2t.md)). Don't re-ask.

**Rules that apply to every assignment here**
- Merge rule [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-11-05-ci-deploy-qoh7ppen.md): merge the building's green PRs and redeploy without asking; migrations ship with the PR; ask Mitchell first only for Bank/token-accounting code or another building's code. CI's promote job redeploys main on green, so an extra `redeploy` call is only needed when promote fails (redeploy churn helped cause the 2026-10-31 CPU-throttle outage).
- Rollup rule (mt_mf00livfrz d.1): only when something visible shipped, a grant closes/checkpoints, a KR was written/edited, or a need only Mitchell can meet; strict four-heading format; Needs never names a gr_/dc_ already in his in-tray.
- Mitchell looks at funding and KRs himself (mt_1u7mwyjrrz d.3); a town "KR met"/"grant adjusted" notice gets `review` approve only.
- Check plans against past rejections (PR #71 hook twice; history page) BEFORE propose_grant.
- GitHub skips CI on a CONFLICTING PR: merge main first (docs/log.md is the usual conflict; keep both entries).
- `tell` refuses user ids. Don't run core and server suites at once on a desk. Time: never write a guessed "~HH:MM"; quote a server stamp or a duration.
