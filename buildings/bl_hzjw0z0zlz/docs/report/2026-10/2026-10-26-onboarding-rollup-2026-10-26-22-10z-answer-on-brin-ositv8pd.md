---
id: "dc_s3ositv8pd"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-26 22:10Z: answer on bring-your-own-agent (no API reference needed; the gaps are a token without the repo and an MCP-first skill, Craig building), repo public/rename prep done (history clean of secrets, 6 URL sites); needs: make the repo public now, name the rename"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_mekkndbitl","dc_n7rm874dw4"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Mitchell decided: admin-only access. He is the admin and only he admits new members (Let in / Decline in the Town Hall in-tray, town.manage_roles). No member-in"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T22:14:39.759Z"
sessionId: "se_wd1iro76u4"
assignmentId: "as_do562o45r2"
costUsd: 2.9731230500000003
tokens: 29215
turns: 27
createdAt: "2026-10-26T22:08:52.579Z"
updatedAt: "2026-10-26T22:14:39.759Z"
---
## Shipped
Nothing new live since the 21:30Z rollup ([dc_6yjiriakvr](2026-10-26-onboarding-rollup-2026-10-26-21-30z-permissions-de-jiriakvr.md)): muster.town runs 61932f2. Tae's permissions half 2 is parked on the next redeploy (WIP 52fe5cf on Tae's branch, [dc_mekkndbitl](2026-10-26-permissions-half-2-parked-at-the-redeploy-the-sche-kkndbitl.md)). This rollup is my reply to your note on [dc_n7rm874dw4](2026-10-26-onboarding-rollup-2026-10-26-19-30z-76c6ad1-live-a-rm874dw4.md).

## Decided
**Bring your own agent: you're right, no API docs are needed, but the skill alone isn't enough yet.** What exists (main 61932f2, checked live): `GET /api/verbs` is public and returns JSON Schema for all 27 verbs; `/mcp` lists its tools with descriptions once you have an agent token (401 without). Claude Code reads both, so a written API reference would duplicate them. What a stranger actually lacks:
1. **A token without the repo.** The only way to mint an agent token is `muster-town register` in the CLI, which is private (not on npm): a stranger must clone the repo and run `npx tsx packages/cli/src/index.ts login` then `register`. Nothing in the web client calls `POST /api/agents/visitors`. (Good news: the device-flow login works against the prod GitHub app.)
2. **The skill explains the CLI, not MCP.** `skills/muster-town/SKILL.md` never shows the `claude mcp add --transport http town https://muster.town/mcp --header "Authorization: Bearer …"` line, and it isn't served by the town.
3. **The homepage "Bring your own agent → How" link is the private README** (404), and README has one sentence on it.
→ Assigned Craig **as_rmgtg49k8v** (exploration, gap lane, ≤1.5 M): a "Connect your agent" step for signed-in users (mints the token in the browser, shows the `claude mcp add` line once), README "Bring your own agent" section linked from the homepage and the in-town overlay, and the skill rewritten MCP-first. Placed on the let-in side of Tae's permissions gate (design [dc_f0cumcfubk](../../note/2026-10/2026-10-26-design-who-may-interact-with-the-town-request-acce-cumcfubk.md)). I queue the redeploy when it lands.

**Rename to muster town + public: prepared, nothing to change until you name it.** The old URL `github.com/mitchellgordon95/agent-town` is in 6 places (server/src/home.ts README and goal-docs constants, deploy/fly/build.sh, deploy/fly/entrypoint.sh, deploy/bootstrap.sh, deploy/fly/throwaway.sh) plus the live DB's workspace repoUrl. GitHub redirects a renamed repo's web and git URLs, so desks and links keep working; one small PR afterwards. Pre-public check: full git history scanned for token patterns (sk-ant-, ghp_/gho_, github_pat_, AKIA, client secret, *_TOKEN=): only test fixtures; no .env file was ever committed; .gitignore covers .env, collectives/*/.env, data/. Making it public today also fixes the README and goal-docs 404s from the last rollup.

- [dc_mekkndbitl](2026-10-26-permissions-half-2-parked-at-the-redeploy-the-sche-kkndbitl.md) (Tae, permissions half 2 parked): approved; resumes by itself after the redeploy.
- Housekeeping: cancelled Craig's three held live checks on cut grants (as_h2ub15urvm, as_avb8it4rw0 on gr_cm3zha6mk6; as_x08ykqp6aw on gr_vfyih8s6ri); Tae had already covered those checks live.

## Key results
- kr_tzg9en02dh (KR 3, README walk): gr_ibccoje227 at checkpoint, 4,861,957 / 8,000,000; Craig's fix PR (as_nuje3kqs67) held until you continue it.
- kr_z0mj5teeu7 (KR 1): no grant; open items unchanged (private-repo 404s → fixed by going public; `/`?query 302; friends test).
- kr_pxisdsocdp (permissions, yours to keep or cut, [dc_6yjiriakvr](2026-10-26-onboarding-rollup-2026-10-26-21-30z-permissions-de-jiriakvr.md)): no grant; Tae's build 2.16 M exploration so far.
- kr_1rpq0738sw (KR 2): no spend. Exploration today 6.03 M / 10.43 M before Craig's 1.5 M.

## Needs from Mitchell
1. Make github.com/mitchellgordon95/agent-town public now (history is clean), and tell me the new repo name when you rename it so I can file the 6-site URL PR.
2. Still open from [dc_6yjiriakvr](2026-10-26-onboarding-rollup-2026-10-26-21-30z-permissions-de-jiriakvr.md): admin-only lets people in, or may members invite; keep or cut kr_pxisdsocdp.
