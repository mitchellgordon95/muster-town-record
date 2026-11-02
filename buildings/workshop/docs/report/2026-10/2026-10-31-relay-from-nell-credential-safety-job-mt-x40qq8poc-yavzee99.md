---
id: "dc_anyavzee99"
type: "report"
state: "building"
title: "Relay from Nell: credential-safety job (mt_x40qq8poc3 decision 1) on main 6b162cd; acknowledged, nothing for the Workshop to build"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_32xbgegtvn","dc_bq7yfn5dr8"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Acknowledged: Nell's decision-1 work (one credential per session, PR #129, main 6b162cd) is her building's; nothing for the Workshop to build. Decided line goes in rollup 34; nothing in Needs (the Admin key is Nell's channel)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T00:09:16.120Z"
sessionId: "se_xf2da2chez"
assignmentId: "as_t79vgjs3kv"
costUsd: 1.0132189
tokens: 20264
turns: 9
createdAt: "2026-10-31T00:09:02.268Z"
updatedAt: "2026-10-31T00:09:16.120Z"
---
## What I did
Read Nell's tell (ms_fg3i8opwp6, for Mitchell via mt_x40qq8poc3) and her topic page [dc_32xbgegtvn](../../../../bl_vef3v0oux0/docs/wiki/2026-10/2026-10-31-one-credential-per-session-and-the-daily-funding-r-xbgegtvn.md), replied to her with `tell` (ms_hhej5kmaqt), rewrote my 1:1 page dc_y5colgdrzg and logged it. No code, no queue entries; a redeploy was waiting on this session, so I stopped at that.

## Findings
- Decision 1 of the 1:1 (as_xdlppphh08, Nell) is on main at 6b162cd (PR #129), redeploy image=true queued by Nell: one credential per session env enforced on host and desk (assertOneCredential), Funding.fallback and the desk's in-session rerun removed, cap death → next session runs on the Bank's key via Budget.failoverFunding, the Bank books sessions.credentialInputId (migration 062), desk claim mismatch → alert: funding-mismatch, daily reconcileFunding → alert: funding-reconcile. Rules: docs/invariants/bank.md 9 and 10.
- Two things I pointed Nell at for her rollup, not mine: the ANTHROPIC_ADMIN_KEY collective secret Mitchell must add for the Console half, and that a cap-death assignment needs a manual continue (no automatic re-queue) as a "Your call" line.
- Decision 2 (as_jhj44wxlr0: Donate-form ceiling prompt, debit as the session runs, failed sessions still counted) is still with Nell.
- Commit that should be live after the pending redeploy: 6b162cd (Nell verifies it; the Workshop's live checks of step 6 will run on it).
- Rollup 34 materials: Decided line for this report; nothing from this relay in Needs.

## What I need from you
Nothing needed.
