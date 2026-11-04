---
id: "dc_ogpz8cgzow"
type: "report"
state: "building"
title: "Hosted collectives with no repo: what Muster-Town-only machinery still shows, and the smallest change that hides it"
authorId: "ag_fbrqt5boxv"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_1vs893enaw"],"urls":[]}
tags: []
verdict: "stop"
decision: "redirect"
decisionNote: "Hide the Muster-Town-only deploy/PR machinery from collectives that have no repo (Mitchell, 1:1 mt_1vs893enaw 11-04: \"collectives that aren't developing Muster Town must not get the redeploy/PR machinery\"). Build the proposal in Pix 3's investigation dc_ogpz8cgzow (read it first; it cites every file:line) as ONE PR off main, no migration, no Bank change: add core `world.repoMode()` → none | own | muster (none = no Town.workspace; own = a workspace whose repoUrl is not this server's own repo; muster = this server's repo). Mode none: `town.redeploy` false for everyone in a hosted World, admins included (permissions.ts); don't register the `redeploy` MCP verb unless mode is muster and the agent can redeploy (server/src/mcp.ts); refuse {deploy} and {pr} waits when work is created and use tool-description variants without them (submit_report, assign, meeting, schedule in schema/src/index.ts; the wait rule in core/src/prompts.ts:34 split so the deploy/PR clause is added only with a repo); REPORT_FORMAT example \"Decide whether X.\" instead of \"Merge PR #12.\" and drop \"merge rights\" from ESCALATION_CRITERIA; drop the \"Live:\" line and make the rollup trigger \"reports were decided since your last rollup\" (keep the 4 h gap); web: hide the Live-build row (PlanSideBar.tsx:96), \"· no code access\" (BuildingPanel.tsx:151) and the disabled code-access checkbox (BuildingPanel.tsx:293). Mode own: keep PR waits, code brief and code access; drop the redeploy line (prompts.ts:665) and {deploy} waits; managers/forks lose `redeploy`, admins and the deployer role keep it. Mode muster: unchanged (this town must behave exactly as today: check the Workshop's own brief still carries the Live line and deploy/PR waits). Leave the hard-coded \"Mitchell\" alone (out of scope, note it in the report). Tests for repoMode and the permission/verb gating in core and server; `npm run check` in the foreground. Open the PR, park on {pr: N}; when green check no migration clash, merge, redeploy, say which commit should be live, and verify on a hosted collective (/<slug>/) that Planning desk → System has no \"Pull main & redeploy\" and an agent's tool list has no `redeploy`."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T18:26:29.547Z"
sessionId: "se_bcsjzezkdn"
assignmentId: "as_wevz4abri7"
costUsd: 0.9919914000000001
tokens: 49600
turns: 22
createdAt: "2026-11-04T18:07:58.685Z"
updatedAt: "2026-11-04T18:26:29.547Z"
---
## What I did
Read-only pass over main 04160f9 (core, schema, server, runtime, web). No code changed.

## Findings
**What "no repo" means today.** A hosted collective's collective.json is written with no `workspace` (server/src/hub.ts:183), so `Town.workspace` is unset and `codeAccess` defaults to off (core/src/store.ts:237). Hosted runtimes run sessions in-process with no desks (runtime/src/index.ts:82). In practice every hosted collective has no repo and can't get one: the repo can only be set in collective.json (core/src/seed.ts:143,213), and there is no UI for it.

**Already hidden (no change needed):**
- The code brief (checkout, branch, PR, "If you call `redeploy`…") only goes to buildings with code access: core/src/prompts.ts:688-690, used at :717-718. Its text is at :655-666.
- Managers and their forks only get `town.redeploy` outside a hosted World (core/src/permissions.ts:66). The hosted runtime has no redeployer and refuses the call (runtime/src/index.ts:761-762, 829-834).
- The PR poller only runs against `workspace.repoUrl` (runtime/src/index.ts:210).
- The merge-rules FYI ([dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-10-30-schema-mi-qoh7ppen.md)) is a document in muster.town's own database. A hosted World's database starts fresh, so it never sees it.

**Still showing (leaks):**
1. **Redeploy button for hosted admins.** The admin role holds every permission (schema/src/index.ts:229), so `store.can("town.redeploy")` is true and Planning desk → System shows "Pull main & redeploy" (web/src/panels/PlanningPanel.tsx:156). Pressing it gets a 403.
2. **`redeploy` MCP tool for every agent.** Every verb is registered with no filter (server/src/mcp.ts:18-20). The tool's description says "Use when Mitchell asks you to deploy" (schema/src/index.ts:2052).
3. **Deploy and PR waits taught to every agent.** The "You can't wait" rule in WORLD_RULES offers `{deploy}` and `{pr}` and points at `GET /api/health` / `git merge-base` (core/src/prompts.ts:34). The same text is in the tool descriptions for submit_report, assign, meeting and schedule (schema/src/index.ts:1909, 1933, 2034, 2036). The wait shape itself is at :782.
4. **`{deploy}` waits fire on muster.town's redeploys.** In a hosted World, `host.commit`/`startedAt` are the hub's own git HEAD and boot time (runtime/src/index.ts:839-851). So `{deploy:"next"}` holds whenever Mitchell redeploys muster.town (core/src/waits.ts:69-71).
5. **`{pr}` waits can never hold.** With no repo there is no PR poller, so a `{pr}` wait expires after 24 h (core/src/waits.ts:83-85).
6. **"Live:" line and the rollup trigger.** The hosted manager's in-tray says "Live: <muster.town commit> (newer than your last rollup)" (core/src/prompts.ts:286-292, 323). Its rollup rule is "roll up when something new is live" (:337). So a hosted manager is told to roll up whenever Muster Town ships, and never because of its own work.
7. **Repo wording in the report and escalation text.** REPORT_FORMAT asks for "PR links" and gives "Merge PR #12." as its example (prompts.ts:42). ESCALATION_CRITERIA mentions "merge rights" (:281).
8. **Smaller web leaks:**
   - Planning stats row "Live build <sha> · redeployed …" shows the hub's commit (web/src/panels/PlanSideBar.tsx:96).
   - The building overview line says "· no code access" (BuildingPanel.tsx:151).
   - Collective defaults shows a disabled "No collective repo" checkbox (BuildingPanel.tsx:293).
9. **Out of scope, worth knowing:** "Mitchell" is hard-coded in manager prompts and in the rollup heading the server enforces ("Needs from Mitchell": prompts.ts:320, 332, 336; schema/src/rollup.ts:95, 128). Hosted managers are told to write to Mitchell.

**Proposal (the smallest set of changes).** Add one core function, `world.repoMode()`, returning one of three modes:
- `none`: no `Town.workspace`.
- `own`: a workspace whose repoUrl is not the server's own repo.
- `muster`: the server's own repo (this town).

There is no new setting: `Town.workspace` already is the "Code repo (optional)" setting.

When the mode is `none` (every hosted collective today):
- permissions.ts: `town.redeploy` is false for everyone in a hosted World, admins included. This one line fixes the button (leak 1) and the verb.
- mcp.ts: don't register `redeploy` unless the mode is `muster` and the agent can redeploy.
- Waits: refuse `{deploy}` and `{pr}` when work is created, and use description variants without them (leaks 2-5).
- prompts.ts:34: split the deploy/PR part of the wait rule into its own clause, added only when there is a repo.
- prompts.ts:42/281: use a neutral example ("Decide whether X.") and drop "merge rights".
- Drop `liveLine`. The rollup trigger becomes "reports were decided since your last rollup", keeping the 4 h gap (leak 6).
- Web: hide the Live-build row, "· no code access" and the code-access checkbox.

When the mode is `own` (a self-hosted collective working on its own repo):
- Keep PR waits, the code brief and code access.
- Drop prompts.ts:665 (the redeploy line) and `{deploy}` waits.
- Managers and forks lose `redeploy` (permissions.ts:66 only applies in `muster`); admins and the deployer role keep it for upgrading the server.
- "Live:" falls back to the reports-decided trigger.

When the mode is `muster`: unchanged.

Rough size: one PR, core and schema plus about 3 web files, roughly 150-250 lines including tests. No migration and no Bank changes.

## What I need from you
Decide whether to make it a grant (the three modes above) or ship just the permissions.ts and prompts.ts:34/337 parts as a small directed fix.
