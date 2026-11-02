---
id: "dc_53wyyztoag"
type: "report"
state: "building"
title: "PR 4 live check, part 1 (curl): homepage serves at 76c6ad1; README/goals links 404 for strangers (repo private); /?guest still 302s; browser half parked until after the redeploy"
authorId: "ag_kc552jb67x"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Your parked continuation (browser half: pitch card, canvas, \"N working now\", screenshots 1400×900 and 390×844, console, guest overlay, /#/grant forward) resumes by itself when the redeploy lands; keep it read-only and under the remaining budget. The private-repo 404s go to Mitchell in my rollup (repo public vs. serving README/goal-directed-budgets from muster.town); don't fix the links yourself."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T19:40:37.679Z"
sessionId: "se_kr2wn803co"
assignmentId: "as_147em8wzdk"
costUsd: 0.36275040000000003
tokens: 11860
turns: 11
createdAt: "2026-10-26T19:10:24.421Z"
updatedAt: "2026-10-26T19:40:37.679Z"
---
## What I did
I ran curl checks against muster.town. Before I could start the headless-Chromium half, a redeploy came in and is waiting on my session, so I stopped and parked the browser checks until the new build is live. No code, no pushes.

## Findings
- **(1) Commit: PASS.** /api/health reports `76c6ad1`, and `git merge-base --is-ancestor 6988a43 76c6ad1` succeeds.
- **(2) Server-rendered `/`: mostly PASS, one FAIL.**
  - PASS: `/` returns 200 text/html with the home bundle tags (`/workshop/assets/home-Cmm3ML6B.js`, `home-FyOIPx09.css`, the overview chunk).
  - PASS: `/api/collectives` returns 200 with 2 entries: the Workshop at `/workshop/`, and "Your collective here" with `placeholder: true` and an empty url.
  - FAIL: the README link and the goal-directed-budgets link both return **404** to anyone who isn't signed in. `github.com/mitchellgordon95/agent-town` is a **PRIVATE** repo (checked with `gh repo view`), so a stranger gets a 404 from both "How" links in "Other ways in" and from the footer README link. This needs one of two fixes: make the repo public, or point the links at pages muster.town serves itself.
- **(4) /api/town: PASS on the API side.** It returned 200 in 0.07 s (33 KB). The canvas and the "N working now" pill still need the browser check.
- **(5) /workshop/: PASS on HTTP.** `/workshop` 302s to `/workshop/`, which returns 200. The guest overlay and the `/#/grant/gr_jqsqra0dlx` forward still need the browser check. The forward script is in the served page: it matches `#/(doc|grant)/` and calls `location.replace("/workshop/"+hash)`.
- **(6) Query on `/`: noted, not fixed.** `/?guest` returns 302 to `/workshop/?guest`, and `/?x=1` returns 302 to `/workshop/?x=1`. Any query string still skips the homepage.
- **(3) the pitch card, the canvas drawing, the screenshots at 1400×900 and 390×844, and the console check are still to do.** I'll run them against the new build when it is live. My desk has no playwright, so I'll install puppeteer-core with /usr/bin/chromium.

## What I need from you
Decide whether to make github.com/mitchellgordon95/agent-town public, or link README and goal-directed-budgets somewhere strangers can open them.
