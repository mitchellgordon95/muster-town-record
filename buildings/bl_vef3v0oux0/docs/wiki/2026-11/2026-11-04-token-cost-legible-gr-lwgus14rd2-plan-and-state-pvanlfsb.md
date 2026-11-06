---
id: "dc_qnpvanlfsb"
type: "wiki"
state: "building"
title: "Token cost legible (gr_lwgus14rd2): plan and state"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vef3v0oux0"
createdAt: "2026-11-04T17:57:51.673Z"
updatedAt: "2026-11-05T20:12:00.698Z"
---
State 2026-11-05 20:12Z (live cd1adc86 since 20:02Z). **Grant gr_lwgus14rd2 AT ITS SECOND CHECKPOINT: 856,858 of 850,000 spent (600k + Mitchell's 250k continue, 19:31Z); checkpoint filed this session (as_4omr5dta38) with a 200,000 top-up asked; first checkpoint [dc_dxz4r8vifo](../../report/2026-11/2026-11-04-checkpoint-gr-lwgus14rd2-lane-token-kind-table-liv-z4r8vifo.md).** Under gl_vjek98yym0 (brief [dc_g7q7s2vug8](../../note/2026-11/2026-11-02-brief-token-cost-is-legible-and-watched-cache-moni-q7s2vug8.md)). Three steps, one PR each, all only read session rows (no Bank or token-accounting change). Both follow-ups are held at the checkpoint: as_hivj114a4v (merge + verify #362) and as_ail5blil47 (merge #364, HUD reads the day's alert from the server, verify).

**Step 1 (kr_pzr1fkgas8, due 11-10): CLAIMED, verified live.** PR #315 (b2282771) + layout fix PR #324 (5ad297d8) verified at 1400×900 ([dc_mw7zg6516p](../../report/2026-11/2026-11-05-gr-lwgus14rd2-step-1-done-lane-kind-layout-fix-5ad-7zg6516p.md), picture mf_464xs0edic); /api/finance/spend?window=7d returns byLaneKind; check:finance 41/41. Code: core `finance-lane-kind.ts`, web `LaneKind` in BankSpending.tsx.

**Step 2 (kr_f49co6lg51, due 11-12): ON-TRACK, redefined by Mitchell (1:1 mt_pr3347g2w2 decision 3): prefix busting.** Old alert #326 (38c3e992) fires live but the HUD's 300-event window never shows it ([dc_lgh99v9tvd](../../report/2026-11/2026-11-05-cache-miss-alert-pr-326-verified-live-in-the-event-h99v9tvd.md)). PR #364 (branch agent/nell/redefine-the-cache-miss-alert-gr-lwgus14): core `cache-miss.ts` `turnUsage`, `sessionBust` (turns 2+, re-write rate = creation/(read+creation) ≥ 0.5; a session busts when most of ≥ 2 such turns do), `cacheMissCheck` per purpose above 0.1 busting share, worst ids named ([dc_7wrr65srdo](../../report/2026-11/2026-11-05-cache-miss-alert-redefined-around-prefix-busting-p-rr65srdo.md)). Live baseline: none of 37 sessions busts. **CI never started on its first push (3947ec76); GitHub gave no run at all.** This session: merged main in (docs/log.md union), CI then failed at check:deadcode (two exports only used in their own files), fixed by un-exporting `sessionKindUsd` and `SessionBust`; head f2894a2d pushed 20:12Z, CI pending. Still a draft; as_ail5blil47 merges it when green.

**Step 3 (kr_avafh64h02, due 11-12): ON-TRACK, built not live.** PR #362 ([dc_wozn4r2688](../../report/2026-11/2026-11-05-gr-lwgus14rd2-step-3-manager-wakes-per-building-pe-zn4r2688.md), branch agent/nell-2/gr-lwgus14rd2-step-3-manager-wakes-per-b): 'Manager wakes' per day in the Spending building drill-down + `managerWakes` in /api/finance/spend + check:finance line. CI never started on its first push (143d3a4d) either; merged main in (mock server.ts import conflict: both `ManagerWakes` and `EngagementView` kept), typecheck + 46 web finance tests green, head 360a69d3 pushed 20:07Z, CI running. as_hivj114a4v squash-merges when green, verifies live.

**Lessons.** A PR whose first push got no CI run: merge main into the branch and push; the synchronize event starts CI. Union-merging a code conflict needs a look (it duplicated an import). After both are verified live: close_grant + rollup.
