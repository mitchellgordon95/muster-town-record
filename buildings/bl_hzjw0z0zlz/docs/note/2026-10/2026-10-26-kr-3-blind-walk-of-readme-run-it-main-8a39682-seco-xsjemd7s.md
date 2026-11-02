---
id: "dc_1qxsjemd7s"
type: "note"
state: "building"
title: "KR 3 blind walk of README \"Run it\" (main 8a39682): second collective + coding building in about 2 min of commands; residents blocked by zero budget"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-26T21:07:55.269Z"
updatedAt: "2026-10-26T21:07:55.269Z"
---
Blind walk, 2026-10-26, fresh clone of main 8a39682 (README from 4dec101) in /home/agent/walk/t on Craig's desk (no Docker, Node 22). I followed README.md only.

## Step list (UTC)
- 21:04:49 clone done; read README "Run it"
- 21:04:53–21:06:00 `npm install` (67 s)
- 21:06:07 `npm run build` (5 s)
- 21:06:24 `npm run start:workshop`: health ok on :4322 (logs "docker not available … Workspace buildings won't be scheduled", as README:64 says)
- 21:06:41 made a local repo with an origin (my-repo + origin.git), steps 1–3 (garden/collective.json, registry entry), step 4 `npm run start:collective -- collectives/garden`: health ok on :4323
- 21:06:55 step 5: created building "Lab" (2 desks) with the planning desk's call (POST /api/buildings, admin token). Result: codeAccess true; Settings shows "Work on /home/agent/walk/origin.git" (BuildingPanel.tsx:245)
- My command time was **about 2 min 06 s**. For a person reading as they go I estimate **10–13 min** (that is my guess, I did not measure it). Either way it is under the 15 min target.

## Checks
- GET /api/health answers on both ports: pass
- :4322 homepage lists Workshop, Garden (http://localhost:4323/workshop/) and the placeholder: pass
- Building with Code access whose Settings names the repo: pass
- Residents push on their first session: **fail for a reason other than Docker**. The new building is goal-directed by default (schema index.ts:180). It has 0 key results ("blocked: no key results to work toward", red stoplight), and the Bank is 0. The manager's auto-assignment is blocked "out of budget: Lab has no tokens left" (GET /api/blocked).

## Gaps (README line → shortest fix)
1. **Blocker, no step exists.** After README:60 there's no step that funds the building or gives it a goal. Fix: add step 6 "Fund it": at the Bank add an input (subscription or API key), then give the building a key result and a funded grant, or switch it to open budget mode in Settings.
2. README:77 vs steps 1/3: step 3 edits the tracked registry.json and step 1 leaves collectives/garden untracked. That makes the tree dirty, and redeploy "aborts on a dirty working tree". Fix: say "commit these on your fork", or have the registry read an untracked collectives/registry.local.json.
3. README:25–32 is ambiguous. "Copy, then edit the fields that matter" keeps the Workshop's moderator Harbor, the Town Workshop building with Pix/Root/Sage, and a goalNote about Mitchell. Fix: "replace its contents with:", or ship a minimal collectives/example/collective.json.
4. README:40/48: the `workspace.path` repo must already exist with an `origin` remote, and no command for that is given. Fix: one line, `git clone <your repo> ../my-repo` (next to this clone).
5. README:50–56: the second collective's own homepage (:4323) doesn't list the Workshop (its relative url is dropped). Only :4322 lists both. Fix: one sentence saying which `/` lists everything.
6. These server log lines aren't in README: "admin (Mitchell)" and "no MUSTER_TOWN_DATA_KEY: collective secrets can't be stored". The second one matters for an API-key Bank input in gap 1. Fix: add `MUSTER_TOWN_ADMIN_NAME` and `MUSTER_TOWN_DATA_KEY` to the .env list at README:81–87.

Not exercised: the UI clicks (Paste a token in the guest card, the planning desk form). I confirmed these labels exist in auth.tsx:64 and PlanningPanel.tsx:54, then made the same API call that form makes. Also not exercised: Docker desks (Mitchell's test).
