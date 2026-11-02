---
id: "dc_vkp2eipsec"
type: "report"
state: "building"
title: "Try now did wake the held work; real bug: an overage rate-limit event re-held everything (PR #254, parked on CI)"
authorId: "ag_kwchpgrsmn"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Retries already done by Pix (as_s3lflvalz2): as_mkzfw2yd64 → as_6w5ulpbb94 (queued); as_7guyfu3buj → as_9af14b4x6k was held \"grant at checkpoint\" (retried checkpoint assignment loses the system author), cancelled; fix PR #255, merge queued as as_zn2voo7zhw. PR #254 merged as dab5b9b and is live since 02:24Z. Folded into rollup 37 (dc_zcuri3xdk2)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T02:26:17.713Z"
sessionId: "se_jp5na7urdv"
assignmentId: "as_kwcmwlabsc"
costUsd: 2.4194915000000004
tokens: 120975
turns: 23
createdAt: "2026-11-02T02:19:10.260Z"
updatedAt: "2026-11-02T02:26:17.713Z"
---
## What I did
Read the live event log (server time 02:12:31Z, live b2b8789) around Mitchell's Try now presses and the three fallback reports. Fixed a real limit bug in PR #254 (draft, CI running). Told Mitchell, Pix and Mara what I found. Updated the topic pages [dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md) and [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md).

## Findings
- **Try now works.** I compared each `bank.limit` "cleared by hand" event with the first `session.started` after it:
  - 01:58:08Z clear → Kelly and Nell started at 01:58:13Z.
  - 01:59:50Z clear → started at 01:59:53Z.
  - 02:02:35/36Z clear → started at 02:02:38Z.

  The runs after the first two presses died within 3–8 s on "You've hit your monthly spend limit", and each death re-recorded the limit (a Fable row with failures 2–3, and a `*` row until 11-04). Most likely the bought credits weren't applied yet, so the Bank page looked as if nothing had woken. After the third press both sessions ran to done: Kelly se_8gwu3m3gnt 600,710 raw tokens, Nell se_en151si4gp 1,561,831.
- **Real bug (fixed in PR #254):** https://github.com/mitchellgordon95/muster-town/pull/254
  - What happened: at 02:06:36Z Pix's running 1:1 session se_px7vadpem2 got a `rate_limit_event` `seven_day_overage_included rejected`. `observeRateLimit` recorded it as an every-model limit until 2026-11-04 00:00Z, so all new work was held again. The session itself kept running on the extra credits. The hold only lifted because Nell's already-running session succeeded at 02:08:55Z; with nothing running, the town would have waited about 2 days.
  - The same pattern on host manage sessions at 21:47–21:48Z shows the limit row flapping between recorded and cleared.
  - The fix: a `rejected` window is now ignored when `overageStatus` is allowed or allowed_warning, or `isUsingOverage` is set (SDK `SDKRateLimitInfo`). Desks now forward both fields, so the desk image needs a rebuild. Added a test to core `availability.test.ts`; typecheck, core availability tests and all 212 runtime tests pass.
  - This is a Bank change. Mitchell asked for the investigation and fix in the 1:1, and I've told him about the PR.
- **Fallback reports, no gap on main.** Three sessions died on the limit and were filed as "Session ended without a report":
  - Mara's as_c02z0e6kht (21:23:58Z, [dc_0mrhdocpxe](../../../../bl_vd69s5a1nh/docs/report/2026-11/2026-11-01-session-ended-without-a-report-write-the-checkpoin-rhdocpxe.md))
  - Pix's as_mkzfw2yd64 (21:23:59Z, [dc_xg29dypbvz](2026-11-01-session-ended-without-a-report-retainers-live-set-29dypbvz.md))
  - Pix's as_7guyfu3buj (21:31:16Z, [dc_gwhoudbufd](2026-11-01-session-ended-without-a-report-write-the-checkpoin-houdbufd.md))

  All three sessions carried credentialInputId bi_5ae13pdi3s. They weren't requeued because the requeue code (faf3eb3) reached main around 21:34–21:39Z and went live only at the 21:47:23Z redeploy. Kelly's death at 21:48:41Z was requeued correctly. gr_5ltmbf3a2f and gr_a5ct690l7a are both still held at their checkpoint with no report filed. The retry route needs building.assign and my agent token doesn't have it (403), so I asked Pix (ms_24eoz6g5f1) and Mara (ms_rsmyq04lsc) to retry them.
- **Live state at 02:12Z:** no open limits on the active input bi_5ae13pdi3s; balance 1,554,705 tokens; 0 free tokens (the 500,000 reserve and open asks take the rest).

## What I need from you
Retry as_mkzfw2yd64 and as_7guyfu3buj (POST /api/assignments/:id/retry). My token can't.
