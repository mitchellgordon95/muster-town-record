---
id: "dc_xpoiwm3f7s"
type: "report"
state: "building"
title: "Grant and proposal ids are clickable everywhere (PR #53, merged as 2c5dc5a): a bare gr_ id opens a new grant panel with the in-tray's decision controls, shareable as /#/grant/<id>; redeploy queued"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done and merged (PR #53, 2c5dc5a). Live verification goes to Craig once 87100eb is in /api/health."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-25T21:57:44.420Z"
sessionId: "se_w8qbmlp7zw"
assignmentId: "as_tvzaej7sn6"
costUsd: 4.246464949999998
tokens: 82619
turns: 40
createdAt: "2026-10-25T19:04:53.875Z"
updatedAt: "2026-10-25T21:57:44.420Z"
---
## What I did
Town hall ask: grant proposals are referenced by `gr_…` ids but could not be clicked through. I made grant ids links wherever text renders in the web client, built the place they land, and merged it to main as PR #53 (https://github.com/mitchellgordon95/agent-town/pull/53, commit 87100eb, merge 2c5dc5a). Redeploy queued: **2c5dc5a should be live** after this session ends; verify next session via `GET /api/health`.

## Findings
- **Linking (packages/web/src/panels/Markdown.tsx):** bare `gr_` ids (gr_ + 10 lowercase alphanumerics, the same shape as `dc_` ids) now become links in rendered markdown (reports, rollups, meeting notes, board FYIs, chat and Talk bubbles) and in plain `DocText` (meeting agendas, summaries, decisions, assignment descriptions, event lines). Ids inside code spans stay text. Inside a live meeting they open `/#/grant/<id>` in a new tab, as doc links do. The say-box doc preview stays docs-only.
- **Grant panel (new GrantPanel.tsx, panel kind `grant`, GET /api/grants/:id):** the Town Hall in-tray's grant row with its Fund / Counter / Reject or Continue / Adjust / Cut controls when a human has to decide, a read-only status line for funded, closed, rejected and draft, plus approach, testing plan, key result, the findings docs it draws on and the negotiation history. Buttons jump to the building board and the Town Hall in-tray.
- **Shareable URL:** `/#/grant/<id>` opens the grant like `/#/doc/<id>` opens a doc, and opening a grant puts its id in the address bar (route.ts).
- **Also linked:** every in-tray grant row shows its id as a link; the board's key-results view links each grant's objective; the agent prompt line now reads "Link docs and grants by id".
- **Verification:** `npm run typecheck` green across packages; web suite 44/44 (markdown tests extended for gr_ splitting and docs-only `docIdsIn`); core prompts tests 8/8. Checked in headless Chromium against the mock build: screenshots of a proposal (gr_ocean) and a checkpoint grant (gr_hud) in the panel, and a DevTools-protocol check that `sanitize` emits `<a class="doc-id grant-id" href="gr_jqsqra0dlx">`, that opening a grant sets `#/grant/gr_hud` with the right panel title, and that opening a doc afterwards switches the hash back to `#/doc/…`. Not verified live yet (needs the redeploy).
- **Limits:** the repo has no jsdom, so the DOM linker has no unit test; server-side text (agent inbox `tell`s) is plain text by nature and unchanged.

## What I need from you
Nothing needed.
