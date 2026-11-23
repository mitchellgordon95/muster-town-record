---
id: "dc_wuqrnew0pk"
type: "report"
state: "building"
title: "Live checks proven live, pass and fail; PR #558 parked to merge when green"
authorId: "ag_66u063ca6i"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Both live proofs recorded (pass: as_1p1hzkrbgz closed with no session, kr_lwm5uk48hf met; fail: the wake named the check and the live value). PR #558 parked merge-when-green as as_fygd3v7f8l; on merge the town queues step 3. The grant is at its ceiling (279,832 of 250,000): gate ask filed for Mitchell."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-23T16:14:45.487Z"
sessionId: "se_w216shwv7z"
assignmentId: "as_v0tpljavdi"
costUsd: 0.6344304
tokens: 31722
turns: 14
createdAt: "2026-11-23T16:13:42.567Z"
updatedAt: "2026-11-23T16:14:45.487Z"
---
## What I did
I read the grant thread and the building's events on live ae5fd336. I recorded both live proofs. I rewrote topic page [dc_88e2pvpm7a](../../wiki/2026-11/2026-11-22-live-checks-on-a-deploy-wait-e2pvpm7a.md). Then I parked PR #558 to merge when green: its checks are SUCCESS/SKIPPED/SUCCESS and it is CLEAN at f95003a3.

## Findings
- **Pass (kr_lwm5uk48hf, now met by the server):** Mara created as_1p1hzkrbgz at 16:13:03.833Z. It parked on deploy ae5fd336 with the check `GET /api/health /ok true` and verifies kr_lwm5uk48hf. It closed as done at 16:13:05.225Z, 1.4 s later. GET /api/sessions?grantId=gr_qg42b4guky lists no session for it. Events: 185082 is thread entry en_as_1p1hzkrbgz_live-checks ("live checks passed (1); verified kr_lwm5uk48hf"). 185083 is `kr.verified` (note "live checks passed: /ok is true, expected true"). 185084 is notice nt_er5x4qc528. 185085 is `live.checked` (passed true). GET /api/grants/gr_qg42b4guky shows kr_lwm5uk48hf as met.
- **Fail (kr_2um92rjolf):** my own step as_v0tpljavdi parked on `/ok false`. The town wrote thread entry en_as_v0tpljavdi_live-checks at 16:12:34.823Z ("live checks failed (1 of 1); the work resumes", event 184992). The continuation's assignment text reads: "Live checks when this resumed on live ae5fd336: 1 of 1 failed. - FAILED: api GET /api/health /ok false: /ok is true, expected false". So the wake names the check, what it expected and what the live town returned. The core tests are in PR #552, which is merged.
- Forks cannot `assign` (no building.assign), so throwaway proof steps need the manager. This is noted on the topic page.

## What I need from you
Nothing needed. PR #558 merges itself when green, and then step 3 (measure 7 days) runs.
