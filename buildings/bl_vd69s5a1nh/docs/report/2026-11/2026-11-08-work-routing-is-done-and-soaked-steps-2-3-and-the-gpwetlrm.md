---
id: "dc_hpgpwetlrm"
type: "report"
state: "building"
title: "Work routing is done and soaked: steps 2+3 and the origin follow-up are live (300072b7), a 4-hour town-wide soak found no misfire; red-main fixer midpoint: no red main in 3 days, nothing fired"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_mdf7hay3eh","dc_u6jxjjuvhx","dc_osu85j8oyx","dc_6colws8gjt","dc_u3d8g27k38","dc_gvdrop9k7b","dc_1bw3ppuyui","dc_u9ac2eq6d4","dc_onx56rapah","dc_c3f19shuo4","dc_tt7r3npm6y","dc_fwa27srwkj","dc_u7ayc5tavx","dc_n6bk8zf1oq","dc_ffmczdp76j","dc_u5p7xy0t9v"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/395","https://github.com/mitchellgordon95/muster-town/pull/396","https://github.com/mitchellgordon95/muster-town/pull/397","https://muster.town/api/health"]}
tags: ["rollup"]
verdict: "stop"
decision: "pending"
sessionId: "se_y1knjsz7xz"
createdAt: "2026-11-08T08:04:27.458Z"
updatedAt: "2026-11-08T08:04:27.458Z"
---
Live: 300072b7 since 2026-11-08 04:49:11Z (CI deploy; it carries our PRs #395, #396 and #397).

## Shipped

**1. Work routing is finished: a forking manager never works a job, and messages to it land in its in-tray**
**What it is:** The rest of the restructure you decided in our 1:1 (mt_lsyqj98z0w). Step 2 (PR #395): a tell, @mention, outbox answer or grant counter/reject sent to a manager with forks becomes a pending row in its building's in-tray, which the manager decides in its next team-lead session; the `managerOnly` bridge is gone; the runtime never starts a work session as a forking manager, and a boot repair moves any leftover rows to the building queue. Step 3 (PR #396) rewrote the docs, AGENTS.md non-negotiable 1 and the team-lead prompt to match. Follow-up PR #397: directed work with no other human origin takes it from its `sourceId`, so its forks' tells carry your origin. Reports: [dc_mdf7hay3eh](2026-11-08-work-routing-step-2-pr-395-opened-manager-wakes-an-f7hay3eh.md), [dc_u6jxjjuvhx](2026-11-08-work-routing-step-2-merged-pr-395-main-5f6571f5-jxjjuvhx.md), [dc_u3d8g27k38](2026-11-08-work-routing-step-3-docs-pr-396-opened-parked-on-c-d8g27k38.md), [dc_gvdrop9k7b](2026-11-08-work-routing-step-3-merged-pr-396-main-b9b14907-drop9k7b.md), [dc_1bw3ppuyui](2026-11-08-work-routing-follow-up-directed-work-takes-its-hum-w3ppuyui.md), [dc_u9ac2eq6d4](2026-11-08-work-routing-follow-up-merged-pr-397-main-300072b7-ac2eq6d4.md); design note [dc_vxsq9g008a](../../article/2026-11/2026-11-08-work-routing-the-target-model-sq9g008a.md) + addendum [dc_wom20h7b9z](../../article/2026-11/2026-11-08-work-routing-step-2-as-shipped-addendum-to-the-tar-m20h7b9z.md).
**What you'd see:** Any building's in-tray (`intray:<building>` on the map, or GET /api/buildings/<id>/intray): a tell or @mention to its manager that traces to a human shows as a pending row tagged `wake:relay` or `wake:mention` until the manager decides it. Every pending row on every building's queue board reads "next free desk"; none is a manager's own. No picture: the probe rows from the live check were decided and have left the in-tray.
**Your call:** A tell or @mention to a manager with no human behind it (origin null, or older than 24 h / past 3 hops) still goes to the inbox only, silently, with no row and no event; say if you want those to leave a row too, otherwise it stays as designed.

**2. The restructure soaked for 4 hours town-wide with no misfire**
**What it is:** A live check at 04:56Z ([dc_tt7r3npm6y](2026-11-08-live-check-2-passed-directed-continuation-s-tell-a-7r3npm6y.md)) proved the new path end to end: a directed continuation's tell to our building and its @mention of me landed as pending wake rows in our in-tray ([dc_fwa27srwkj](2026-11-08-message-from-mitchell-via-mara-1-live-check-2-prob-a27srwkj.md), [dc_u7ayc5tavx](2026-11-08-mentioned-by-mara-1-for-mitchell-note-live-check-2-ayc5tavx.md)). Then a one-shot soak ([dc_u5p7xy0t9v](2026-11-08-routing-4-hour-soak-no-misfires-0-manager-work-ses-p7xy0t9v.md)) replayed every live event from step 1 going live (03:53:40Z) to 08:00:24Z, 954 events with no gaps, and read all 7 buildings' in-trays and queues.
**What you'd see:** In that window: 31 sessions started, 16 of them manager sessions, all `purpose: manage` with no assignment, 0 manager work sessions. 14 jobs named a forking manager; all 14 went to a building queue, 13 ran on forks, 1 is correctly held (Workshop as_62lpwynu0z, "grant at checkpoint"). 3 wake rows written, 0 still pending, 0 dropped by the caps; 5 origin-less tells from sessions that started before #397 went to the inbox by design. 0 queue-repair events, 0 error or warning events on wakes, in-tray or createAssignment. API/event evidence only, no screen changed.
**Your call:** None.

**3. Red-main fixer (gr_7op2v8fjcl) midpoint: 3 days of main with no red, so nothing fired, which is right**
**What it is:** The grant's step 3 is a 7-day observation. Its midpoint ([dc_ffmczdp76j](2026-11-08-gr-7op2v8fjcl-midpoint-no-red-main-since-ed953de-w-mczdp76j.md)) scanned the last 200 main CI runs and 16,869 live events since the fixer went live on 11-05 00:08Z. 62 green runs, one failed run (4ab6187c, 11-05 23:18Z) whose `check` and `image` passed and only the `promote` push to prod was refused by GitHub; `mainStateOf` counts that as not red, so no fixer was named. 0 fix assignments, 0 duplicate fixes by humans or agents.
**What you'd see:** GET https://muster.town/api/health `main` at 07:00:22Z: `{state: green, sha: 300072b7, failedStep: null, fixer: null}`. The final 7-day check runs on 11-12 07:00Z (sc_ylx02vdi8z); if it is also clean I close the grant with that evidence and the unspent tokens return to the Bank.
**Your call:** None.

## Decided
- [dc_mdf7hay3eh](2026-11-08-work-routing-step-2-pr-395-opened-manager-wakes-an-f7hay3eh.md) → approve (step 2 PR #395 opened; merge continuation parked on CI)
- [dc_u6jxjjuvhx](2026-11-08-work-routing-step-2-merged-pr-395-main-5f6571f5-jxjjuvhx.md) → approve (PR #395 merged → 5f6571f5; Pix told)
- [dc_osu85j8oyx](2026-11-08-session-ended-without-a-report-work-routing-step-3-u85j8oyx.md) → redirect (step 3 fork ended without a report; retry told to check the desk's git status first)
- [dc_6colws8gjt](2026-11-08-routing-step-2-live-at-5f6571f5-since-04-18-09z-no-olws8gjt.md) → redirect (step 2 live at 5f6571f5, no manager-own rows; in-tray path not exercised because the probe tells carried no human origin → origin follow-up #397)
- [dc_u3d8g27k38](2026-11-08-work-routing-step-3-docs-pr-396-opened-parked-on-c-d8g27k38.md) → approve (docs PR #396 opened from the stashed edits, two text fixes)
- [dc_gvdrop9k7b](2026-11-08-work-routing-step-3-merged-pr-396-main-b9b14907-drop9k7b.md) → approve (PR #396 merged → b9b14907)
- [dc_1bw3ppuyui](2026-11-08-work-routing-follow-up-directed-work-takes-its-hum-w3ppuyui.md) → approve (PR #397 opened: directed origin from sourceId)
- [dc_u9ac2eq6d4](2026-11-08-work-routing-follow-up-merged-pr-397-main-300072b7-ac2eq6d4.md) → approve (PR #397 merged → 300072b7)
- [dc_onx56rapah](2026-11-08-live-check-2-repeat-pr-397-main-300072b7-not-live-x56rapah.md) → approve (live check-2 repeat parked on the #397 deploy)
- [dc_c3f19shuo4](2026-11-08-live-check-2-repeat-300072b7-live-but-this-session-f19shuo4.md) → approve (300072b7 live; parked 2 min so the continuation carried an origin)
- [dc_tt7r3npm6y](2026-11-08-live-check-2-passed-directed-continuation-s-tell-a-7r3npm6y.md) → approve (live check 2 passed)
- [dc_fwa27srwkj](2026-11-08-message-from-mitchell-via-mara-1-live-check-2-prob-a27srwkj.md) → approve (probe wake:relay row)
- [dc_u7ayc5tavx](2026-11-08-mentioned-by-mara-1-for-mitchell-note-live-check-2-ayc5tavx.md) → approve (probe wake:mention row)
- [dc_n6bk8zf1oq](2026-11-08-mentioned-by-mara-1-for-mitchell-report-live-check-bk8zf1oq.md) → approve (mention row for [dc_tt7r3npm6y](2026-11-08-live-check-2-passed-directed-continuation-s-tell-a-7r3npm6y.md))
- [dc_ffmczdp76j](2026-11-08-gr-7op2v8fjcl-midpoint-no-red-main-since-ed953de-w-mczdp76j.md) → approve (gr_7op2v8fjcl midpoint clean; my approve note's text was garbled by a leaked tool call, the decision stands)
- [dc_u5p7xy0t9v](2026-11-08-routing-4-hour-soak-no-misfires-0-manager-work-ses-p7xy0t9v.md) → approve (4-hour soak clean; nothing to queue)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_7op2v8fjcl red-main fixer | kr_mvj61meiwx main's CI state in /api/health | claimed ([dc_ypesutja1t](2026-11-05-gr-7op2v8fjcl-9f2d28f-is-live-and-api-health-main-esutja1t.md)) | ≈662,000 / 1,000,000 (606,795 at the 11-06 read + 55,782 for the midpoint session; re-read at the 11-12 final) |
| gr_7op2v8fjcl | kr_hsfxuz8tnx one named fixer per red main | on-track (code live; no red main yet to exercise it) | — |
| gr_7op2v8fjcl | kr_09nhvvwc1a 7-day no-duplicate-fix window | on-track (midpoint clean; final sc_ylx02vdi8z 11-12 07:00Z) | — |
| work routing (directed, mt_lsyqj98z0w) | no grant: all steps live, checked, soaked | done | directed today 731,611 |

Spend today by lane: exploration 0 tokens (11,196,971 free under the goal), directed 731,611 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 2 proposals (gr_baf19xtg7p, gr_sczsxd9ztm), 0 requests, 1 rollup ([dc_fhv9gez4iy](2026-11-08-work-routing-step-1-is-live-pr-394-3320f44f-a-job-v9gez4iy.md))._
