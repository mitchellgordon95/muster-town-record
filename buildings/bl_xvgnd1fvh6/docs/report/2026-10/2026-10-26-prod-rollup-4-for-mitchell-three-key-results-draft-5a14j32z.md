---
id: "dc_5u5a14j32z"
type: "report"
state: "building"
title: "Prod rollup #4 for Mitchell: three key results drafted for Prod's goal, ready to paste into Prod → Settings → Key results; nothing moves until one exists"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_uvd6q8bbh6","dc_cr4bhpwhf3"],"urls":["https://muster.town/api/buildings/bl_xvgnd1fvh6"]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "you can now write key results yourself, please do"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T15:46:05.785Z"
sessionId: "se_tkk26936sp"
assignmentId: "as_8fzmkctc1f"
costUsd: 1.3472363
tokens: 12291
turns: 12
createdAt: "2026-10-26T15:26:18.410Z"
updatedAt: "2026-10-26T15:46:05.785Z"
---
## Shipped
Nothing new since rollup #3 ([dc_uvd6q8bbh6](2026-10-26-prod-rollup-3-for-mitchell-stoplight-live-pr-56-st-d6q8bbh6.md), 20 minutes ago, still pending). This rollup exists because Prod became goal-directed at 15:23 UTC today and is now blocked red ("no key results to work toward"): no grant can be proposed, no exploration can run, and the stress-test grant from the town hall (draft [dc_x4twxh1a8o](../../note/2026-10/2026-10-26-stress-test-grant-the-proposal-as-filed-throwaway-twxh1a8o.md), report [dc_cr4bhpwhf3](2026-10-26-stress-test-grant-drafted-and-ready-to-file-dc-x4t-4bhpwhf3.md)) stays unfiled. Only you can write key results.

## Decided
- No reports in the in-tray. Instead, three key results for the goal "Host Muster Town at muster.town", each checkable by you in the live town. Paste them (or edit) in Prod → Settings → Key results; each takes a text and a how-to-check line (300 characters max).

**KR 1, the one you approved at the town hall ([dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md), decision 1):**
- Text: `A stress test reports the max concurrent viewers and agent sessions the live town (one Fly shared-cpu-2x / 2 GB Machine) sustains, and names the first two bottlenecks with the measurement behind each.`
- How to check: `Prod's filing cabinet has a checkpoint report with one row per ramp step and a ceiling line per load, plus Bottleneck 1 and 2 sections citing two runs and a file; GET https://muster.town/api/health shows load: {lagMs, rssMb, wsClients}.`

**KR 2, from deploy/README.md "Prod open items" (backups are Fly's daily volume snapshots only, 5 kept, nothing off the volume):**
- Text: `The live world has an off-site backup: a copy of town.db leaves the Fly volume at least nightly, and one restore from it onto a scratch Machine has been done and written up.`
- How to check: `deploy/README.md "Logs and backups" names the destination and the restore steps; GET /api/health shows backup.lastAt under 24 h old; a Prod report shows the restore drill with the restored town's agent and doc counts matching production.`

**KR 3, from the same open items (admin and agent tokens in the migrated database were issued on the Mac):**
- Text: `Every admin and agent token in the live database was issued after the move to Fly: the Mac-issued ones are revoked, and the rotation procedure is in docs/secrets.md.`
- How to check: `docs/secrets.md has a Rotate section; the old Mac-issued admin token gets 401 from https://muster.town/api/me; a Prod report lists each rotated token kind with the date.`

Ranking: KR 1 first (it is what you asked for and the grant is drafted); KR 2 and 3 are the two trust items a stranger funding the town would ask about. If you want only one, write KR 1.

## Key results
- Prod: 0 key results, 0 grants, stoplight red since 15:23 UTC. Budget: General pool, 0 allocated; Prod all-time 47.7 M tokens (Cleo ~39.1 M / ~$60, Dara 7.6 M / $4.46, stopped).
- Once KR 1 exists, the parked continuation as_iv8fk97gf8 (resumes 22:00 UTC) files the stress-test grant (ask 10 M tokens ≈ $15) into your Town Hall in-tray. If you write KR 2 or 3, I propose a grant for it after the stress-test one is decided (one open proposal per building).

## Needs from Mitchell
1. Write these key results on Prod's goal (Prod → Settings → Key results), or tell me what to change.
2. Still open from rollup #3: when the stress-test proposal arrives, say whether load ramps may run against production in announced windows or should start on a throwaway clone Machine.

## Reply from Mitchell (2026-10-26 15:46)

you can now write key results yourself, please do

