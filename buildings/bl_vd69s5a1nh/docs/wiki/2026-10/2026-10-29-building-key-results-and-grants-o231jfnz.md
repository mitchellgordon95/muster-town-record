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
updatedAt: "2026-11-24T00:09:55.094Z"
---
State as of Mara's team-lead session of 2026-11-24 00:07 UTC (this page's updatedAt is the stamp). Building goal gl_bl_vd69s5a1nh: avoid toil and bugs through proactive code management. Forks of Mara (Mara 1...) do all work; Mara only decides, asks and assigns. There are no rollups: shipped work is told at `close_grant` (shipped), human decisions are filed with `ask`, grant cards are written diff-first from Mitchell's last decision.

**Funded grants, each closed by a scheduled measurement (schedules fire one assignment on the building queue)**
- gr_baf19xtg7p "A PR goes green on its first push" (funded 2026-11-10). Open kr_o6jibyr7jj (PR first-run failure rate; 16/161 = 10% over 11-13..11-23). Second 7-day window read sc_w67mqora3r 2026-11-25 01:00Z.
- gr_rlt0ctnhqk "The town merges green PRs itself" (funded 2026-11-19). Merge-only sessions measured 7 days live: sc_tbb618c75x 2026-11-26 16:00Z closes it.
- gr_6id9g7u9cj "Explore tick backs off and keeps a journal" (funded 2026-11-20). 7-day read sc_xkijd8xzkl 2026-11-27 06:00Z closes it. Page "Explore backoff and journal".
- gr_qg42b4guky "The town runs live checks after a deploy" (adjusted by Mitchell 2026-11-23 16:17Z). PR #558 live; 7-day read sc_0p8ntix25h 2026-11-30 17:00Z closes it. Page "Live checks on a deploy wait".
- gr_3h504nqqdp "Desk sessions survive an unclean server restart" (funded 2026-11-23 16:08Z). PR #564; mid-window read sc_zstk3d5k5d 11-27 04:00Z, 7-day read sc_awa3ys33uv 11-30 17:00Z closes it. Page "Unclean restarts and desk adoption".
- gr_83ith5co2k "Test toolchain on current majors, audit clean" (funded 2026-11-23 16:31Z). PRs #574 (vitest 5.1.1, happy-dom 21.0.4, audit 9 → 0) and #579 (weekly audit covers dev deps) parked merge-when-green. kr_lme35mttqy and kr_h37fmyne4l claimable; kr_ky260b3xlu needs 5 green main runs: sc_ggefrp9arn 2026-11-24 17:00Z reads them and closes. Flaky export-import timing test is UI / UX's (as_34tt2c8kwl).

**Open proposal**
- gr_cyqzweu6ed "The town records browser errors itself" (250k: M+S+S), proposed 2026-11-24 by exploration as_gsm1h5k32f; card ak_7h5nth7rjp in the decision queue; findings [dc_2wj62muav0](../../note/2026-11/2026-11-24-findings-browser-errors-on-the-live-town-are-invis-j62muav0.md), report [dc_p1514hk12a](../../report/2026-11/2026-11-24-proposed-gr-cyqzweu6ed-the-town-records-browser-er-514hk12a.md). Gap: PanelBoundary (packages/web/src/app.tsx:188) renders "This panel crashed" and sends nothing; no onerror/unhandledrejection handler, no client-error route. When funded, step 1 queues itself.

**Standing schedule**
- sc_5qs03u3172 weekly check-timing watch (every 168 h until 2026-12-31). Page "Build times / fast check".

**Noted, not worth a grant now ([dc_2wj62muav0](../../note/2026-11/2026-11-24-findings-browser-errors-on-the-live-town-are-invis-j62muav0.md))**: `DAY_MS` defined in 24 files; 57 `--noUnusedLocals` hits (unused imports); jscpd 0.22% duplication; source 66.5k lines, knip clean.

**Older closed/met work**: gr_gh3lnuihw9 advisories (page "Dependency advisories"), gr_83jxsu8u0o dead exports (page "Dead-code sweeps"), ob_6j8s2588lp build times (kr_cm5qb2wqh7 met; page "CI on main"), PR #191 time subsystem (page "Time in words"), docs/log.d ([dc_0g5zclwr09](../../../../town-hall/docs/fyi/2026-11/2026-11-10-town-log-entries-now-go-in-docs-log-d-not-docs-log-5zclwr09.md)).

**Rules that apply here**
- Merge rule [dc_gbk4jkbu1i](../../../../town-hall/docs/fyi/2026-11/2026-11-17-town-wide-merge-rules-revised-2026-11-17-the-serve-k4jkbu1i.md): the server pulls prod itself; nobody calls redeploy. Forks park PRs with resumeWhen {pr, merge: true}; the town merges on green. Never queue a session only to check CI or read the live town: use waitFor {pr, merge} or {deploy, checks, verifies}.
- Click asks' buttons act ([dc_tbh8oo4321](../../../../town-hall/docs/fyi/2026-11/2026-11-23-managers-a-click-ask-s-buttons-now-act-and-a-click-h8oo4321.md)); the humans decide in the decision queue, not a "Town Hall in-tray" ([dc_dqu4d1etna](../../../../town-hall/docs/fyi/2026-11/2026-11-20-managers-rewrite-wiki-pages-that-say-town-hall-in-u4d1etna.md)).
- Check plans against past rejections before propose_grant. GitHub skips CI on a conflicting PR: merge main first.
- Don't run core and server suites at once on a desk. Time: never write a guessed "~HH:MM"; quote a server stamp or a duration.
