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
updatedAt: "2026-11-25T01:07:24.858Z"
---
State as of Mara's team-lead session of 2026-11-25 01:0x UTC (this page's updatedAt is the stamp). Building goal gl_bl_vd69s5a1nh: avoid toil and bugs through proactive code management. Forks of Mara (Mara 1...) do all work; Mara only decides, asks and assigns. There are no rollups: shipped work is told at `close_grant` (shipped), human decisions are filed with `ask`, grant cards are written diff-first from Mitchell's last decision.

**Funded grants, each closed by a scheduled measurement (schedules fire one assignment on the building queue)**
- gr_baf19xtg7p "A PR goes green on its first push" (funded 2026-11-10). Work done. Second window ([dc_gid54je37c](../../report/2026-11/2026-11-25-second-window-after-499-first-run-ci-failures-8-2-d54je37c.md)): 8 of 97 first runs failed, 8.2% (7.3% without deliberate #580), target under 6%; knip and docs failures 0. kr_sbqqx7548z and kr_vcv244638c hold. kr_o6jibyr7jj is with Mitchell as a click ask (Missed / Met); when he decides, close_grant it (closing first would mark the KR met, grants.ts closeDone; an ask on a met-unverified KR is refused, asks.ts:537). PR #601 (check:css into the hook) merges itself: as_favuo21lnv waits {pr 601, merge}.
- gr_rlt0ctnhqk "The town merges green PRs itself" (funded 2026-11-19). sc_tbb618c75x 2026-11-26 16:00Z closes it.
- gr_6id9g7u9cj "Explore tick backs off and keeps a journal" (funded 2026-11-20). sc_xkijd8xzkl 2026-11-27 06:00Z closes it. Page "Explore backoff and journal".
- gr_qg42b4guky "The town runs live checks after a deploy" (adjusted 2026-11-23 16:17Z). PR #558 live; sc_0p8ntix25h 2026-11-30 17:00Z closes it. Page "Live checks on a deploy wait".
- gr_3h504nqqdp "Desk sessions survive an unclean server restart" (funded 2026-11-23 16:08Z). PR #564; mid-window sc_zstk3d5k5d 11-27 04:00Z, 7-day sc_awa3ys33uv 11-30 17:00Z closes it. Page "Unclean restarts and desk adoption".
- gr_cyqzweu6ed "The town records browser errors itself" (funded 2026-11-24 21:47Z). PRs #592, #599; step 3 parked on deploy be1d9885 with live checks for kr_prvi7xacqh; sc_rdzgemh0o6 2026-12-02 17:00Z reads 7 days and hands me the close (kr_lr3buf0v8n). Page "Browser errors (client-errors)".
- gr_83ith5co2k "Test toolchain on current majors, audit clean" (funded 2026-11-23 16:31Z): check its state on the grant page before touching it; sc_ggefrp9arn (2026-11-24 17:00Z) was to read 5 green main runs and close.

**Standing schedule**: sc_5qs03u3172 weekly check-timing watch (every 168 h until 2026-12-31). Page "Build times / fast check".

**Noted, not worth a grant now ([dc_2wj62muav0](../../note/2026-11/2026-11-24-findings-browser-errors-on-the-live-town-are-invis-j62muav0.md))**: `DAY_MS` defined in 24 files; 57 `--noUnusedLocals` hits; jscpd 0.22%; source 66.5k lines, knip clean. Docker image "fatal: not a git repository" first-run failures (2 in the window) are a CI context issue, not hook-catchable.

**Older closed/met work**: gr_gh3lnuihw9 advisories, gr_83jxsu8u0o dead exports, ob_6j8s2588lp build times, PR #191 time subsystem, docs/log.d ([dc_0g5zclwr09](../../../../town-hall/docs/fyi/2026-11/2026-11-10-town-log-entries-now-go-in-docs-log-d-not-docs-log-5zclwr09.md)).

**Rules that apply here**
- Merge rule [dc_gbk4jkbu1i](../../../../town-hall/docs/fyi/2026-11/2026-11-17-town-wide-merge-rules-revised-2026-11-17-the-serve-k4jkbu1i.md): the server pulls prod itself; nobody calls redeploy. Forks park PRs with resumeWhen {pr, merge: true}. Never queue a session only to check CI or read the live town: use waitFor {pr, merge} or {deploy, checks, verifies}.
- A missed key result: only a human marks it (building.fund). File a click ask on the kr_ (branches Missed / Met, body must say who waits) before close_grant, and close after the decision lands in the in-tray.
- Click asks' buttons act ([dc_tbh8oo4321](../../../../town-hall/docs/fyi/2026-11/2026-11-23-managers-a-click-ask-s-buttons-now-act-and-a-click-h8oo4321.md)); the humans decide in the decision queue ([dc_dqu4d1etna](../../../../town-hall/docs/fyi/2026-11/2026-11-20-managers-rewrite-wiki-pages-that-say-town-hall-in-u4d1etna.md)).
- Check plans against past rejections before propose_grant. GitHub skips CI on a conflicting PR: merge main first. Don't run core and server suites at once on a desk. Never write a guessed "~HH:MM"; quote a server stamp or a duration.
