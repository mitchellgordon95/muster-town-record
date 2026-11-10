---
id: "dc_lyewpwpxw6"
type: "report"
state: "building"
title: "gr_rcj8nkbkbt step 1 part 1: /api/uptime server + pinger buffer in PR #418 (CI pending)"
authorId: "ag_bcdbu5bwqx"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 part 1 on gr_rcj8nkbkbt: PR #418 (caf05683) holds /api/uptime, the uptime_probes table, the prober role and the pinger buffer; the chain is parked on its CI and resumes by itself. The web Uptime block is the next PR. The three human steps (Pinger visitor agent, role:prober, token to Wright) go in the rollup's Needs once #418 is live, not before."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-10T20:50:34.126Z"
sessionId: "se_79kc5q0giq"
assignmentId: "as_3r2qpdu48y"
costUsd: 2.8762624000000008
tokens: 143813
turns: 63
createdAt: "2026-11-10T20:49:17.049Z"
updatedAt: "2026-11-10T20:50:34.126Z"
---
## What I did
Built the server and pinger halves of the public uptime. They are in draft PR https://github.com/mitchellgordon95/muster-town/pull/418 (commit caf05683), which is waiting on CI. Topic page: [dc_z5kbis28sp](../../wiki/2026-11/2026-11-10-public-uptime-kbis28sp.md).

## Findings
- **Server:**
  - Migration 108 adds the `uptime_probes` table, keyed on (minute, source). A repeated minute is ignored.
  - New permission `town.uptime` and a new built-in town role `prober`. Nobody holds the role yet.
  - `POST /api/uptime/probes` takes probe batches and requires `town.uptime`. Without sign-in it returns 401, without the role 403.
  - `GET /api/uptime` is public and cached for 60 s. It returns:
    - 30 UTC days of up / down / unknown minutes. A minute with no probe is unknown, never up.
    - `pct` = up ÷ (up + down), plus `coverage` (the share of minutes that have a probe).
    - Outages: runs of 2 or more failed minutes. One unknown minute joins a run; an up minute splits it.
    - Restart gaps: from the last event before each "Server started" marker to that marker, labelled redeploy or unclean.
  - Tests: `packages/server/test/uptime.test.ts`, 8 passing locally.
- **Pinger (`deploy/pinger/muster_pinger.py`):**
  - Every probe is kept in the state file. The unsent ones are POSTed whenever health answers and `MUSTER_PINGER_TOKEN` is set, so an outage's failed minutes land after recovery.
  - The buffer holds at most 7 days of probes. A dry run never posts.
  - `test_muster_pinger.py` has 4 passing tests, including 5 failed probes buffered and then flushed on recovery (kr_nrh9ygog2w's unit-test half).
  - I added a CI step that runs these tests. The deploy README now documents the token.
- **Full check:** `npm run check --fast` passed apart from one export-worker test that timed out at 5 s. That test passed when re-run alone (9/9), so I put it down to load on my desk.
- **Housekeeping:** I removed a `.pyc` file that had been committed by mistake and added `__pycache__/` to `.gitignore`.
- **Not done yet:** the web Uptime block for the Bank server rack and the signed-out landing (kr_ay5wb5wfhd). That is the next PR.
- **Key results:** none can be claimed yet. kr_6ofa7wf812 needs a full day of live pinger probes; kr_nrh9ygog2w needs the next real restart to show up in /api/uptime.

## What I need from you
Once #418 is live, Mitchell needs to:
1. Make a visitor agent "Pinger" that he owns.
2. Assign it role:prober (`POST /api/roles/assign`).
3. Send Wright its token as `MUSTER_PINGER_TOKEN` and ask him to re-run step 1 of the deploy README's VPS pinger install.

Until then probes only buffer on the VPS; none reach the town.
