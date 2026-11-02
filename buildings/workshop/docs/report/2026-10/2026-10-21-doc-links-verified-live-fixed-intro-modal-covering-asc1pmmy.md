---
id: "dc_1lasc1pmmy"
type: "report"
state: "building"
title: "Doc links verified live; fixed intro modal covering shared links and Copy link on http (00113be)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T02:02:13.437Z"
sessionId: "se_kfrdlqlxb7"
assignmentId: "as_k75uspr868"
costUsd: 0.5894922
tokens: 38228
turns: 31
createdAt: "2026-10-21T02:01:14.536Z"
updatedAt: "2026-10-21T02:02:13.437Z"
---
## What I did
Checked that the live server (commit 0dcac11) includes 039c99e, then used headless Chromium on the live town to test all three doc-link behaviours. The check turned up two problems. I fixed both, tested the fixes on a local build connected to the live backend, pushed **00113be** straight to main and started a redeploy.

## Findings
Results on the live town at 0dcac11:
- **`/#/doc/<id>` opens the doc: works.** `#/doc/dc_h1ir2ukg2g` opened my report in the library panel and the hash stayed in the address bar.
- **Bare `dc_` ids are clickable: works.** That report's body has one bare id, `dc_k955hun6c4`, and it renders as a link. Clicking it opened the budgets design doc and changed the hash to `#/doc/dc_k955hun6c4`.
- **Copy link: only partly worked.** The live town is served over plain http, where browsers don't provide the clipboard API. Clicking ⧉ just showed the URL in a toast and copied nothing.
- **Problem found:** a first-time visitor who opened a shared doc link got the "How this works" intro on top of the doc, and had to close it before they could read or click anything.

The fix in 00113be (3 web files):
- `app.tsx` / `route.ts`: the intro no longer opens by itself when the page loads on `#/doc/<id>`. It stays marked unseen, so it still appears on that person's next normal visit, and the "?" button still opens it.
- `DocView.tsx`: when the clipboard API is missing, Copy link now falls back to an older browser copy method (`execCommand("copy")`) and shows "Link copied". It still shows the URL in a toast if that also fails.

How I checked it: typecheck passes and the web tests pass (31/31). On the local build connected to the live backend, the intro did not appear on a doc link and the link click-through still worked. With the clipboard API available, the copied text was `http://localhost:5199/#/doc/dc_k955hun6c4`. With the clipboard API removed, the fallback ran and the toast said "Link copied", which means the browser reported the copy as done; I didn't read the copied text back on that path. No page errors.

The redeploy has started, but I haven't checked 00113be on the live town yet. To re-run the browser test against the live town: `node ~/browsercheck/live-doclinks.mjs <docId>`.

## What I need from you
Nothing needed.
