---
id: "dc_zrsy5gno60"
type: "report"
state: "building"
title: "PR #261: CI was red from main's own breakage; fixed in the PR, ready, parked on CI again"
authorId: "ag_amv53b4a85"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Main's red (manual 23 words over cap, four unused exports) was fixed in #261 at 3373c627 with no behaviour change; note main at 024b236 (Mara's PR #250 merge) now carries the same two fixes (07895b6, a3f17c1), so expect a trivial overlap at merge, nothing more. Continuation as_pifiz1snn2 already waits on {pr: 261}; nothing else to queue."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-02T03:29:55.197Z"
sessionId: "se_tjc8subgkn"
assignmentId: "as_5plg2z9stq"
costUsd: 0.6614077
tokens: 33070
turns: 20
createdAt: "2026-11-02T03:29:41.168Z"
updatedAt: "2026-11-02T03:29:55.197Z"
---
## What I did
PR #261 (https://github.com/mitchellgordon95/muster-town/pull/261) failed CI, but not because of its own code. Main has been red since three recent commits from other buildings (f72fe630, 01ccc8ed, 88bcbf36), and that also means nothing is deploying.
- I merged main into the PR and fixed main's breakage in commit 3373c627, with no change in behaviour.
- The full `npm run check` passes locally: docs, dead code, typecheck and all tests (7m32s).
- I marked the PR ready for review and parked until its CI finishes.
- I told the Onboarding and Workshop managers so they don't push a competing fix. Kelly is idle and will only see it in their next session.

## Findings
- **What was red on main:**
  - `docs/manual.md` was 1923 words, 23 over the 1900-word cap. The cause is Onboarding's hosted-starter-key line.
  - The dead-code check flagged `HOSTED_CAP_LINE` (web BankFunding.tsx), `FounderRoad` (server hub.ts), and `HelpThing` and `HelpCard` (web helpCard.ts). All four are used only inside their own files.
- **The fix:**
  - I tightened the manual's "Your API key" bullet and its "Getting a key" paragraph down to exactly 1900 words. The facts stay: 1,000,000 tokens (about $20), work stops, talk still runs. I cut the side notes "billed to you" and "the token stays on your server".
  - I removed the four unused `export` keywords.
  - This edits other buildings' code, but only to make main's CI pass again; it changes nothing they do.
- **No change to the step-1 work itself.** The status→outcome mapping and the expected sentence are as in [dc_roe9bv2x8u](2026-11-02-spending-tab-says-what-each-grant-bought-step-1-pr-e9bv2x8u.md).

## What I need from you
Nothing needed.
