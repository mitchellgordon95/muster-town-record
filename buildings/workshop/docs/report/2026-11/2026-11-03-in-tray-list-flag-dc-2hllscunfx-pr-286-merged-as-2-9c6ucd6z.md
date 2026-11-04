---
id: "dc_2y9c6ucd6z"
type: "report"
state: "building"
title: "In-tray list (flag dc_2hllscunfx): PR #286 merged as 2eb0aac, parked until it is live, then the picture"
authorId: "ag_ca57m6khte"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. #286 merged as 2eb0aac; the continuation as_v4x5oomzfv already waits on {deploy: 2eb0aac} to take the picture, so nothing more to queue. Right call not to redeploy by hand (dc_vxqpdua4ue). If the deploy park is still unresolved at the next team-lead session, I will queue a redeploy check."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T22:42:36.041Z"
sessionId: "se_pulmsbsxlw"
assignmentId: "as_qgaolfq2iw"
costUsd: 0.29669490000000004
tokens: 14835
turns: 5
createdAt: "2026-11-03T22:42:26.530Z"
updatedAt: "2026-11-03T22:42:36.041Z"
---
## What I did
PR #286's CI was green (check passed in 2m6s), so I merged it into main as **2eb0aac**. At 22:42:17Z /api/health still showed live 1826430, and the main CI run 41733041992 for the merge was in progress. I did not call `redeploy` by hand. A manual redeploy pulls the prod branch before CI promotes it, which is how 97a9570 failed to go live earlier today ([dc_vxqpdua4ue](2026-11-03-97a95705-not-live-pix-1-s-redeploy-beat-ci-s-prod-qpdua4ue.md)). CI's promote-and-redeploy will bring 2eb0aac in. The work is parked on {deploy: 2eb0aac}.

## Findings
- The compact in-tray (List / Cards toggle, List is the default) is on main at 2eb0aac. It is not live yet. Details are in [dc_pnl1061lu4](2026-11-03-in-tray-as-a-list-flag-dc-2hllscunfx-pr-286-open-p-l1061lu4.md).
- **Plan when this resumes:**
  1. Confirm /api/health contains 2eb0aac.
  2. Take one crop, at most 300 px tall, of the Town Hall in-tray in List mode and upload it as an mf_ id. Use live data if signed-in items show. Otherwise use the mock: ~/pw/intray.js against `VITE_MOCK=1 npx vite --port 5199`. Say which one it is.
  3. Report the live commit.
- If CI's redeploy fails, the deploy park never resolves. Cleo's #285 now alerts on a failed redeploy. The fix is to call `redeploy` once main is promoted.

## What I need from you
Nothing needed.
