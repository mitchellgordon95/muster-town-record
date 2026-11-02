---
id: "dc_8kwh69dc0q"
type: "report"
state: "building"
title: "BYOA without the repo: parked for the waiting redeploy; Connect panel WIP on my branch (d52d9df), not on main"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked continuation resumes after the redeploy I'm queuing now; plan (api.ts + mock, wire /#/connect, GET /skill.md, README_REPO constant, MCP-first SKILL.md, README section, tests, local proof, screenshots) stands. Note Mitchell confirmed admin-only access: your \"Ask to join first\" state matches db3534a's AuthMe.canInteract."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T22:33:50.265Z"
sessionId: "se_xyzrt2njnf"
assignmentId: "as_rmgtg49k8v"
costUsd: 1.018163
tokens: 48034
turns: 24
createdAt: "2026-10-26T22:09:24.758Z"
updatedAt: "2026-10-26T22:33:50.265Z"
---
## What I did
- Read the style guide ([dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)) and Tae's access design ([dc_f0cumcfubk](../../note/2026-10/2026-10-26-design-who-may-interact-with-the-town-request-acce-cumcfubk.md)). Tae's branch adds `AuthMe.canInteract` (default true) but doesn't touch web yet.
- Wrote `packages/web/src/panels/ConnectAgent.tsx`: a dark-chrome panel (it's working UI). It has three states: a guest gets "Sign in to connect your agent", a signed-in person who isn't let in gets "Ask to join first", and everyone else gets a form (name defaults to "<login>'s Claude", optional building). The form calls `POST /api/agents/visitors` and then shows the `claude mcp add --transport http town <origin>/mcp --header "Authorization: Bearer …"` line once, with a copy button and a link to the skill.
- A redeploy interrupt arrived while I was working, so I stopped. The work in progress is committed on my branch only, as d52d9df (`agent/craig/bring-your-own-agent-without-the-repo-we`). It is not wired in yet, and main is unchanged.

## Findings
- No live change from me. The commit that should go live with the waiting redeploy is 497a43b, my README fix from the last session.
- Remaining plan (also in my wiki):
  - api.ts and mock `registerVisitor`.
  - Wire up the panel: PanelKind "connect", `/#/connect`, a link in the HUD's signed-in row, and the How-this-works line.
  - Serve the skill without the repo: `GET /skill.md` serves `skills/muster-town/SKILL.md`. This closes the "can't get the skill without cloning" half of the gap.
  - home.ts: derive the How link from a single `README_REPO` constant, pointing to `#bring-your-own-agent`.
  - Make SKILL.md MCP-first and write the README section.
  - Tests, then local proof (register in the UI, curl `tools/list`) and screenshots.
- I've used about 0.1 M tokens of the 1.5 M budget.

## What I need from you
Nothing needed. The work resumes on its own after the redeploy.
