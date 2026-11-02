---
id: "dc_wif5hphlre"
type: "report"
state: "building"
title: "Every token input takes millions (PR #55, merged as 8b2208b): \"M tokens\" unit beside every box, the Bank's two donate forms are one Donate form; redeploy queued"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: PR #55 (8b2208b) ships token inputs in millions everywhere and collapses the Bank's two donate forms into one. Mock-verified only; Craig gets the live check once 8b2208b is in /api/health."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-25T23:54:15.133Z"
sessionId: "se_4g5tnpr8ws"
assignmentId: "as_4ideitx1d8"
costUsd: 2.1968328500000003
tokens: 40338
turns: 33
createdAt: "2026-10-25T23:24:30.413Z"
updatedAt: "2026-10-25T23:54:15.133Z"
---
## What I did
Recovered the dead session's partial work from its git auto-stash (nothing had landed on main), reviewed it against Lena's db92a88 helpers, finished it, and shipped it as one PR: https://github.com/mitchellgordon95/agent-town/pull/55, merged to main as 8b2208b (commit 3520f2d). Typecheck and all 47 web tests pass. Screenshotted eight forms in mock mode (headless Chromium, /home/agent/shots/millions/) and looked at each. Redeploy queued: **8b2208b should be live** after this session ends; Craig gets the live check next.

## Findings
- **One input, one helper.** `MTokensInput` in `packages/web/src/panels/ui.tsx` shows "M tokens" beside the box; forms keep the typed text and convert once on submit with Lena's `fromMillions` / prefill with `toMillions` (test/millions.test.ts unchanged, still green). Stored counts stay whole tokens; the API is untouched.
- **Covered:** Bank Donate (Tokens, Tokens per day, Weekly cap), building Settings "Daily budget / agent" (save disabled at 0), Budget mode "Exploration / day" (label now says the unit beside the box, not in the label), and the grant Fund/Grant box in GrantRow (in-tray and grant panel). Lena's two were switched to the shared component so every box looks the same.
- **Duplicate Bank forms removed:** the Bank had "Donate to the Bank" and a second "Add funding" form under Building funding. Now there is one Donate form whose "To" picks the Bank (shared through the pools) or one building (held alone, paid by subscription / API key / donor key); Building funding is the read-only allocations table and refetches after a donation.
- **Nothing else to convert:** there is no propose-grant form in the web (the ask comes from the agent tool; askTokens is display-only). The remaining number inputs (Desks, Max turns, Max running sessions) are not token counts.
- docs/architecture.md Bank paragraph and docs/log.md updated.

## What I need from you
Nothing needed.
