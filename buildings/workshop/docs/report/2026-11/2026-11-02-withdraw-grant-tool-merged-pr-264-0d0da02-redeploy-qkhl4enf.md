---
id: "dc_0tqkhl4enf"
type: "report"
state: "building"
title: "withdraw_grant tool merged (PR #264 = 0d0da02), redeploy queued"
authorId: "ag_p4ucp3vjge"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "withdraw_grant merged as 0d0da02; the main snapshot at 024b236 (live since 03:38Z) contains it, so it is live. Live check queued separately."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T03:38:49.637Z"
sessionId: "se_8mgan1gsmi"
assignmentId: "as_r8wz26kata"
costUsd: 1.5346859000000002
tokens: 76734
turns: 11
createdAt: "2026-11-02T03:38:27.841Z"
updatedAt: "2026-11-02T03:38:49.637Z"
---
## What I did
Built the `withdraw_grant` town tool (1:1 mt_a6wb51enia) and merged [PR #264](https://github.com/mitchellgordon95/muster-town/pull/264) as **0d0da02** after green CI, then queued a redeploy, so 0d0da02 should be live next. I dropped the "withdraw gr_kph1zjjrzg" step as Pix asked, because Mitchell already rejected it, and proposed nothing. I rewrote topic page [dc_oghes5lgud](../../wiki/2026-10/2026-10-28-grants-key-results-and-the-town-hall-in-tray-hes5lgud.md) with the withdraw rule.

## Findings
- **Who and when:** the manager of the grant's building (or a fork acting for it), or a human who can fund the grant, withdraws a draft, proposed or countered grant. A note saying why is required. A funded or checkpoint grant is refused with a pointer to `close_grant` or a human's cut. Another building's manager is refused.
- **What happens:**
  - The grant closes with outcome `stopped` and history action `withdraw`.
  - The note stays on the grant: the grant panel's History shows "withdrew the proposal" with the note.
  - The note also goes to the inbox of every human who can fund the grant.
  - The grant leaves the Town Hall in-tray and the review deck, and its ask is freed.
  - Its open key results archive like a rejected proposal's.
  - The `grant.closed` event carries `{withdrawn: true, note}`.
- **API route:** `POST /api/grants/:id/close` with outcome stopped on a proposal now goes through the same path. Before, its key results were left un-archived.
- **Prompt and docs:** the manager prompt (core prompts.ts) gets one line ("withdraw_grant…, then propose_grant fresh"). docs/how-work-gets-done.md gets a "Withdrawing a proposal" paragraph.
- **Tests and checks:**
  - New test in core/test/lanes.test.ts covers the manager allowed, another manager refused, funded refused, in-tray and deck rows gone, key results archived, the note in history, the event and the funders' message, and countered → withdraw → fresh propose.
  - Locally: core 664/664 and typecheck green. CI `check` passed in 3m12s.
  - Server tests not run locally: the change adds no route, and the CI check passed.
- Not live-checked yet: the redeploy was only queued this session.

## What I need from you
Nothing needed.
