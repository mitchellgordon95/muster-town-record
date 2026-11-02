---
id: "dc_yk3s2n4qf8"
type: "report"
state: "building"
title: "Building settings are a thin layer on goals: Name (optional), Attached to, Desks and Manager in one form; planning desk loses Managers (PR #157, c899aa8, redeploy queued)"
authorId: "ag_ilcfy1gjo7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_n25udpflus","dc_vzqoh7ppen","dc_jcyf86dpdp"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/157"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: PR #157 merged c899aa8, redeploy queued. Live check queued as a separate assignment; as_siu3ksjrhn (collective defaults) now starts on its own."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T05:06:59.780Z"
sessionId: "se_bi99gqowm6"
assignmentId: "as_z7cdbryk1k"
costUsd: 4.2740716
tokens: 213704
turns: 96
createdAt: "2026-10-31T05:06:49.459Z"
updatedAt: "2026-10-31T05:06:59.780Z"
---
## What I did
After the redeploy, here is what Mitchell sees. **A building's Settings** opens with one form: **Name** (optional; the placeholder reads "defaults to the goal's short text"), **Attached to** (the goal picker, now part of the form), **Desks** and **Manager**. The hint under Manager says a building made at the planning desk gets its manager when it is built. Below those are the model, budget and code-access fields, then Bank pool and Exploration budget, all unchanged; the follow-up assignment moves them. The Goal and Description text boxes are gone, and so are the separate "Attached to" section and its Attach button. One **Save settings** saves everything. The Overview's goal card shows the attached goal's text.

**The planning desk** now has the tabs Buildings | Roles | Secrets | System. The Managers tab is gone. Each building row shows its goal path, desk count and ★ manager, and clicking a row opens that building's Settings. **New building** asks for Goal, then Name (optional), then shows the default Desks. The Purpose box is gone.

PR: https://github.com/mitchellgordon95/muster-town/pull/157. I merged it as **c899aa8** and queued a redeploy, so c899aa8 should be the live commit. I have not checked it live.

Crop of the new Settings form (mock data, scaled to 300 px): mf_3y4cmm7wit. A 1:1 crop of Name and Attached to: mf_qlj72gbv49.

## Findings
- **Name rule:** a blank or missing name becomes the attached goal's text, cut to 40 characters at a word boundary with "…" (core `Goals.defaultName`). This applies when a building is created and again on every save where the name is left blank, using the current goal (or the new one if the same save moves it). A name typed by hand stays when the goal moves. Every place that shows a name keeps working, because the name is stored.
- **Goal and description text dropped:** the create and update requests for buildings (`CreateBuildingInput` / `UpdateBuildingInput`) no longer accept `goal` or `description`. If a request sends them, they are ignored. The database columns stay; there is no migration. `seed.ts` and `import-v0` still pass the text from old collective.json specs.
- **Purpose is the attached goal everywhere:** core `Goals.purposeOf(b)` now feeds:
  - the desk brief's "Building goal:" line (the Workshop's brief will stop saying "Ship improvements…" and name the Steer goal it is attached to)
  - the meeting facilitator's brief
  - the board header and `look`
  - the export README
  - the "blocked building" assignment text
  - `/api/kpis` and the board's `goal` field

  In the web client, `purpose.ts` reads it from the goal's `plaza:<goalId>` place (Overview, map side bar, map sign). The Overview no longer shows the old description.
- **Checks:** `npm run check --fast` passes after merging main twice, the dead-code step passes, and all 43 web test files pass.
  - New tests: core `building-thin-layer.test.ts` covers the request no longer taking goal text, the brief line, `look`, and the name rule in all its cases. Two new tests in web `planDesks.test.tsx` cover the form order with no textareas, and the planning desk with no Purpose box and rows that open Settings.
  - Updated tests: server `rest.test.ts` (a name-less create returns 201 named after the goal, and an over-long name returns 400) and `grants.test.ts`.
- **Docs:** I updated `docs/manual.md`, `docs/architecture.md` and `docs/log.md`. The manual had to stay under its 1,900-word cap, so I also replaced the stale sentence about resizing buildings on the town map with one saying the map is drawn from the goal tree. I rewrote the topic page [dc_jcyf86dpdp](../../wiki/2026-10/2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md).
- **Not checked:** nobody has seen this live yet. Next session's check: `/api/health` should show c899aa8, and a guest opening Workshop → Overview should see the Steer goal text.

## What I need from you
Nothing needed.
