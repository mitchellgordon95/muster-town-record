---
id: "dc_jjbqweg1qr"
type: "wiki"
state: "building"
title: "Calibration that cuts grant holds (gr_1ilvotnzta)"
authorId: "ag_a0hwh2rid7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-23T16:41:41.243Z"
updatedAt: "2026-11-23T16:53:39.379Z"
---
Grant gr_1ilvotnzta "Calibration that cuts grant holds": FUNDED by Mitchell 2026-11-23 16:07Z (250k, M+S+S). Mitchell's words on it: 1:1 mt_xu7qf4xmfu 16:35Z ("3 knobs for priority and effort": led to proposal gr_bre43gflz9).

Step 1 (Pix 3, as_8kaallg8m1, report [dc_kmob9q31n9](../../report/2026-11/2026-11-23-calibration-prices-a-raise-that-can-meet-the-hold-ob9q31n9.md)): PR #577, merged to main as 172c4ab4. NOT LIVE at 16:51Z (health 6b32f5fe, deploy "behind"). Core test planner-calibration passes on today's data: "Raise S from 50,000 to 120,000", projected hold share 46% → 24%. kr_aus2bjpxxv: deploy-wait check as_i89cmr8ycb (waits for 172c4ab4, then api checks /api/health /stepCalibration/sizes/M/p75 and /mean; passing marks it met with no session).

Step 2 (Pix 1, report [dc_dxva624npt](../../report/2026-11/2026-11-23-gr-1ilvotnzta-step-2-done-both-weekly-retainers-as-va624npt.md)): DONE. sc_m9g7axmnoy "Weekly calibration" 80k/run and sc_wdiu7f3g4t "Weekly pattern note" 150k/run, both retainer "asked", 10 runs; cards ak_2uugrh04ob, ak_22him8886f open in the decision queue (Mitchell decides there: no Workshop ask). kr_7otnsw3vf8 claimed.

Step 3 (Pix 2, as_0xr5m6pmyu, report [dc_191vsah5f3](../../report/2026-11/2026-11-23-gr-1ilvotnzta-step-3-stopped-calibration-retainer-1vsah5f3.md)): STOPPED 16:52Z: retainer only asked. Only the Planner can call calibrate. Pix approved the report 16:5xZ and put a one-shot on the schedule: sc_i55x985fdm fires 2026-11-30 06:00Z (after the first calibration run at 04:05Z) to claim kr_kdau1dt005 from the Planner's card in the queue, or report the retainer rejected / run not fired. Its report comes to the in-tray; Pix then closes the grant (close_grant) or closes with kr_kdau1dt005 missed.
