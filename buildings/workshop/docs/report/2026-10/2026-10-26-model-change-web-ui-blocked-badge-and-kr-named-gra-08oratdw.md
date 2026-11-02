---
id: "dc_3s08oratdw"
type: "report"
state: "building"
title: "Model change web UI: blocked badge and KR-named grant rows pushed to main 16690b0; parked for the live check"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "16690b0 is on main and included in the live build (9b20fad is live); your parked continuation does the live check. Also verify the flag badge rows on the building in-tray while you're there (as_sk61n57yqf)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T04:28:00.133Z"
sessionId: "se_m297lur3ar"
assignmentId: "as_tatcakwm1m"
costUsd: 1.6422356999999996
tokens: 112535
turns: 49
createdAt: "2026-10-26T00:05:15.314Z"
updatedAt: "2026-10-26T04:28:00.133Z"
---
## What I did
- Read Lena's core report ([dc_h2v9eyyrhh](2026-10-25-model-change-core-pushed-to-main-c07cd95-krs-on-th-v9eyyrhh.md)) and Cleo's ([dc_d9qc5l5dwt](../../../../bl_xvgnd1fvh6/docs/report/2026-10/2026-10-25-key-results-are-on-the-building-board-pr-54-merged-qc5l5dwt.md)). Cleo's a04acaf had already shipped item 1 (the Settings → Key results editor) and item 4 (the board's KR view, which reads status off the goal). I built what was left of items 2 and 3 in packages/web.
- Pushed straight to main as **16690b0** and requested a redeploy. `npm run typecheck` passes, and web tests pass 50/50 (3 of them new, in test/keyResults.test.ts).

## Findings
- **Blocked state (item 3).** A goal-directed building with `blockedAt` set now shows "Blocked: no key results" in three places:
  - **Building panel → Overview:** the label, plus one line on who unblocks it: a human writes the goal's key results in Building → Settings → Key results. A human who can manage the building also gets a link to Settings.
  - **Map sign:** an extra red line.
  - **Town Hall in-tray:** a new "Blocked" section at the top that lists each blocked building and how long it has been blocked. It is not counted in the badge.
- **Bug fixed along the way.** The web client was throwing away the in-tray's `blocked` field, so blocked buildings could never have shown there. It keeps it now, and the mock in-tray returns it too.
- **Grants (item 2).** In the in-tray and grant panel, each grant row now says "Key result:" with the one key result it names and that result's status, followed by its testing plan. If a proposal names no key result, Fund is disabled and the row says why: counter it so the manager names one. Token inputs still take millions.
- **Proposal form.** There is no web proposal form. The manager proposes through the `propose_grant` tool, which already requires a key result.
- **Live state.** The Workshop's `blockedAt` is set on the live server (2026-10-25T18:41:44Z), so once 16690b0 is live it should show blocked until Mitchell writes its key results.
- Docs updated: docs/goal-directed-budgets.md (UI section) and docs/log.md.

## What I need from you
Nothing needed.
