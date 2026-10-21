---
id: "dc_1xhda8m14m"
type: "report"
state: "building"
title: "Talk bubbles render markdown with single-newline breaks (on main, redeployed)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T17:54:17.352Z"
sessionId: "se_7tmzr0dkd7"
assignmentId: "as_axomqtpum9"
costUsd: 0.3874815
tokens: 503680
turns: 17
createdAt: "2026-10-20T17:23:48.616Z"
updatedAt: "2026-10-20T17:54:17.352Z"
---
## What I did
I checked that Root's drain-then-restart redeploy is on main (commits 280d204 and 6a787e9), then redid the Talk-bubble markdown change. I pushed it straight to main as a0adb1c, following the standing rule, and started a redeploy so the server pulls and restarts.

## Findings
- **Change:** both bubble types in the Talk tab now use the shared `Markdown` component instead of plain text: messages to and from an agent, and quick-question replies. They are sanitized the same way, and doc links open in the library.
- **New `breaks` option on `Markdown`:** a single press of Enter now shows as a line break. It is off by default, so documents still wrap single newlines as before.
- **Styling:** there is a new `.md.bubble` style in `packages/web/src/styles.css`. It sets normal white-space inside the bubble's `pre-wrap` box, trims the first and last margins, and uses smaller headings and inline code.
- **Code:** `packages/web/src/panels/Markdown.tsx` now has an exported `markdownHtml(text, breaks)`. `AgentPanel.tsx` imports `Markdown` and uses it for both bubble types.
- **Checks:** `npm run typecheck` passed. The web tests passed (17/17), including the new `packages/web/test/markdown.test.ts`, which covers the default soft wrap, `<br>` with `breaks`, and lists and bold text with `breaks`. `vite build` passed.
- **Not checked:** I didn't look at the bubbles in a browser.
- **No PR:** the standing rule says to push to main. The branch `agent/sage/hold-the-talk-bubble-markdown-work-markd` is also on the remote at the same commit.

## What I need from you
Nothing needed.
