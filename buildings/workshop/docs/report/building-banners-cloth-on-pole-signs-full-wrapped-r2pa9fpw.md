---
id: "dc_ifr2pa9fpw"
type: "report"
state: "building"
title: "Building banners: cloth-on-pole signs, full wrapped goal, click opens settings (f43647c on main, awaiting redeploy)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T21:38:03.484Z"
sessionId: "se_crct3ud9ue"
assignmentId: "as_18t9ue3scs"
costUsd: 0.9527545000000002
tokens: 1740042
turns: 40
createdAt: "2026-10-20T21:34:49.263Z"
updatedAt: "2026-10-20T21:38:03.484Z"
---
## What I did
Restyled the building signs as banners and made them clickable. Pushed f43647c straight to main and queued a redeploy. It wasn't live after about 5 minutes (health still showed 98cdae4), so this is parked until the deploy lands. When it resumes I'll check the change in the live town.

## Findings
- **Look** (`packages/web/src/map/overlay.ts`, `drawSign`): the plain dark box is now a red cloth banner. It hangs from a wooden rod with gold-capped ends, held up by two posts. It has loops at the top, a dashed stitched border and a notched bottom edge, with the name in cream, the goal in gold and the budget line in green. The cloth gets brighter on hover.
- **Full goal**: the 56-character cut-off in `renderer.ts` is gone. A new `wrapText` wraps the goal across lines 200–280 px wide, and the banner grows upward to fit.
- **Click**: the renderer now records where each banner is on screen. In `MapCanvas.tsx`, hovering a banner shows a pointer cursor, and clicking one opens that building's panel on its Settings tab. People who can't manage the building get the Overview tab instead. Clicking an agent still opens the agent, and agents win if they overlap a banner.
- **Checks**: `npm run typecheck` passes and the web tests pass (27/27). In the mock UI with headless Chromium, the Town Hall, Carbon Cycle Lab and Workshop banners drew with their goals wrapped. Clicking the Town Hall banner opened "Town Hall → Settings". Not yet checked in the live town.
- No PR: the workshop's standing rule is to commit straight to main. A line was added to `docs/log.md`.
- **Security note**: while looking for the server URL I printed my desk's environment variables, which put the town token and the fallback API key into this session's transcript. Nothing was sent anywhere else, but rotating those two may be worth it.

## What I need from you
Nothing needed; the work picks up again by itself once f43647c is live.
