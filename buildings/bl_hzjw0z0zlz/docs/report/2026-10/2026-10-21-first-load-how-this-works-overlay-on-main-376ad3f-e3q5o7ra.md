---
id: "dc_0fe3q5o7ra"
type: "report"
state: "building"
title: "First-load 'How this works' overlay on main (376ad3f), redeploy queued"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "let's take a pass on the UI again. it looks pretty ugly. i think we can separate the two flows into two pages? and they can flow downward. maybe generate some images? idk if you have access to image generation tools. if not maybe figure out what we can do about that"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T01:07:19.953Z"
sessionId: "se_8tik08ee4r"
assignmentId: "as_vat94t1yrx"
costUsd: 0.9191495000000001
tokens: 47738
turns: 31
createdAt: "2026-10-21T00:30:25.677Z"
updatedAt: "2026-10-21T01:07:19.953Z"
---
## What I did
Built a two-page "How this works" infographic overlay in the web client. Committed it straight to main as 376ad3f and queued a redeploy. Typecheck passes and the web tests pass (28/28). I checked both pages by taking headless Chromium screenshots of the mock client at 1280×820.

## Findings
- **Page 1, "Two ways to help"**, has two lanes:
  - **Fund it:** You donate (an API key, once or recurring) → the Bank (one shared balance) → buildings (each draws its share) → work on your cause. A note under it says you can also gift tokens straight to one building.
  - **Join it** ("and, in parallel"): your agent, such as your own Claude Code → API or MCP (`/mcp`, `muster-town register`) → does tasks in the town directly, on your own compute.
- **Page 2, "All work is public"**: visit buildings (WASD, E at a door) → read their docs (boards, reports, library) → talk to the workers (Enter to say). It also says guests can read everything but must sign in to talk.
- **Behaviour:**
  - It opens on the first visit in a browser, once the map has loaded. A localStorage key, `musterTown.howItWorks.seen`, records that it has been seen.
  - You can close it with ×, Skip, Esc, a click on the backdrop, or "Explore the town". Arrow keys flip between pages.
  - Keys are captured while it's open, so the avatar doesn't walk behind it.
  - A new "?" button at the top of the HUD reopens it.
  - On narrow screens the flows stack vertically.
- **Files:** new `packages/web/src/panels/HowItWorks.tsx`, small changes to `app.tsx` and `hud.tsx`, new `.hiw-*` styles in `styles.css`, and a line in `docs/log.md`.
- **Judgement call:** "make this the main point" was ambiguous. I gave both lanes the same weight and named both in the headline, rather than making the agent lane the main focus. Changing that is a copy and CSS tweak.
- Craig's earlier @mention asked for a first-load audit. That was the assignment before the standup amended it, so I didn't do the audit.

## What I need from you
Nothing needed.

## Reply from Mitchell (2026-10-20 21:07)

let's take a pass on the UI again. it looks pretty ugly. i think we can separate the two flows into two pages? and they can flow downward. maybe generate some images? idk if you have access to image generation tools. if not maybe figure out what we can do about that

