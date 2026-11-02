---
id: "dc_ltrn24ufw5"
type: "report"
state: "building"
title: "Town Hall in-tray verified live on b569636; the newline bug was a stale tab (PR #44 was live), so the client now reloads itself after a redeploy (867dc3f on main)"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Mitchell asked why Kelly's five reports reached him individually instead of being rolled up. Cleo investigates: confirm whether reports from meeting-decision as"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-25T14:34:19.636Z"
sessionId: "se_p4jx9fze37"
assignmentId: "as_ocwmzgbu4r"
costUsd: 3.11907085
tokens: 61449
turns: 36
createdAt: "2026-10-24T23:31:04.161Z"
updatedAt: "2026-10-25T14:34:19.636Z"
---
## What I did
- Checked the live site: `/api/health` reports b569636 (waterfall step 3), so the redeploy Mitchell approved had already run; nothing to trigger.
- Drove https://muster.town in headless chromium over CDP from my desk (script ~/livecheck/nl.mjs, method in skill [dc_p70ti5mkvn](../../../../../library/skill/2026-10/2026-10-24-live-ui-check-0ti5mkvn.md)): opened the Town Hall in-tray panel and meeting mt_p8mo4bsrsy, and inspected the rendered HTML of Mitchell's utterance.
- Found the real cause of the newline report and shipped a fix on main: commit 867dc3f (draft PR #47 closed in favour of the main commit after a rebase onto Kelly's #46). Typecheck, 35 web tests and the web build are green. docs/log.md updated.

## Findings
- **Town Hall in-tray is live.** On b569636 the client's places include `intray:town-hall` ("Town Hall in-tray (rollups, proposals, checkpoints)") and `openPanel("intray","town-hall")` renders the In-tray panel with 1 item waiting (my rollup [dc_jkbed7u3fo](2026-10-24-prod-rollup-1-for-mitchell-fly-cutover-verified-pr-bed7u3fo.md)). Lena's own verification ([dc_zmtf9iznsd](../../../../workshop/docs/report/2026-10/2026-10-24-town-hall-in-tray-checked-in-the-browser-on-live-b-tf9iznsd.md)) agrees.
- **Newlines already render in the meeting transcript.** On the live b569636 bundle, Mitchell's utterance that contained the complaint renders as four separate `<p>` elements at distinct vertical positions (bubble height 188 px, `white-space: normal` with paragraphs from `marked` `breaks: true`). That behaviour shipped in PR #44 (518b4e4, live on ca5bd27 since about 22:00 UTC); before it the transcript was a plain `div` that collapsed newlines. Mitchell reported the bug at about 23:05 UTC, so his tab was most likely loaded before that deploy.
- **Root cause: tabs never pick up a new build.** After a redeploy restarts the server, the client reconnects its WebSocket, refetches events and toasts "redeploy done", but keeps the old JavaScript bundle indefinitely. Every UI fix we ship is invisible to an open tab until a manual reload.
- **Fix (867dc3f):** `api.ts` gains `health()` (on the `Api` interface, HttpApi and MockApi). `app.tsx` records the server commit at boot; on a WebSocket reconnect it fetches health again and calls `location.reload()` when the commit differs. If a text box with content has focus it shows the toast "A new version of the town is live. Reload the page to get it." instead, so nobody loses a half-typed message.
- **Deploy state:** main = 867dc3f, prod = de4474b (CI was mid-way through deploying #46); a redeploy was draining behind my session (Root, Kelly, Cleo). CI should deploy 867dc3f after that. I'll verify it live next session, and the self-reload the first time a redeploy runs with a tab open.

## What I need from you
Nothing needed. Mitchell: if you still see collapsed newlines in a meeting transcript, reload the tab once; after 867dc3f is live that happens by itself.
