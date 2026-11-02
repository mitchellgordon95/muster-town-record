---
id: "dc_e8tgzb2t3b"
type: "article"
state: "building"
title: "Design note: all sessions run server-level, desks on demand"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["design","runtime","desks","sessions"]
createdAt: "2026-10-23T04:30:48.460Z"
updatedAt: "2026-10-23T04:30:48.460Z"
---
For @Mitchell, from standup decision 2 (mt_g9cesvdc0d). I wrote this from the code on main at 34cc56c, and file references are repo-relative. The four numbered questions at the end are the parts that need your call.

## 1. What a server session can do today

The runtime has three kinds of session. Only the desk kind has a shell or a checkout.

| Session | Code path | Tools |
|---|---|---|
| Work (host backend) | `runtime/src/work.ts` runWorkSession → `session.ts` runAgentSession | Town MCP verbs plus WebSearch/WebFetch. Bash, Read, Write, Edit, Glob, Grep, Task and Agent are blocked (`DISALLOWED_TOOLS`). **It refuses any building with code access** (`codeWorkspace` check), so Workshop work never runs here. |
| Facilitator | `meetings.ts` facilitate → runAgentSession | Town verbs only (`web: false`). |
| Meeting summary, meeting reply, proxy chat, "ask about" | `oneShot` in `sdk.ts` | **No tools at all.** It is one cheap model call. The runtime posts the text through the `meeting` verb for the model. |
| Desk work | `desk/session.ts` runDeskSession → `agent-town-desk run` in a container or Fly Machine | Full Claude Code with `bypassPermissions`, the repo checkout from `desk/src/workspace.ts` (clone, fetch, session branch), and town verbs over HTTP `/mcp`. |

One correction to the standup: meeting replies are not tool sessions. The fast standup is a set of one-shots plus one tool-using facilitator. A server-level 1:1 or work session with real tools would be a runAgentSession, which costs more turns but has the same instant start.

The host plumbing to build on is already there: runAgentSession with streaming input and interrupts, the `HostHooks` pattern for runtime-backed verbs (`redeploy` works this way: `core/src/world.ts` HostHooks → `core/src/verbs/admin.ts`), and park/resume through `submit_report` `resumeWhen`.

## 2. Proposal in one line

Every session starts as a host runAgentSession. A desk becomes a resource that a session picks up through four tools. Real code changes still run as a desk assignment with native Claude Code. The server session hands that work off; it does not drive the edits over RPC.

## 3. The desk toolset (four new verbs)

The verbs go in `VerbInputs`. They are runtime-backed through a new `HostHooks.desk`, like redeploy. They are available only when the agent's building has a workspace (`codeWorkspace`) and a desk backend is up (`world.host.docker`).

- **`desk_start {branch?}`** → `{cwd, branch, head}`
  - Calls `backend.ensure(agent, building)`, then runs a new `agent-town-desk prepare --session <id>` (only `workspace.ts`, no Claude) so the checkout exists and is fetched.
  - Idempotent: a second call returns the same desk.
  - The default branch is the session's own `agent/<name>/…` branch, like desk sessions today.
- **`desk_run {command, waitSeconds≤120 (default 30), cwd?}`** → `{runId, done, exitCode|null, output, truncated}`
  - Starts the shell line in the background as the `agent` user and waits up to `waitSeconds`.
  - `output` is the last 16 KB, clipped.
  - Env: git auth (`gitAuthEnv`) and the agent's granted secrets (`grantedSecrets`). **No model keys**, because nothing in the desk calls Claude.
- **`desk_output {runId, offset?, waitSeconds?}`** → `{done, exitCode, output, nextOffset}`
  - Pages through a long run (tests, build).
  - Same chunked log and exit-file protocol `desk/fly.ts` FlyApi.run already uses (`/tmp/run-<id>.log` and `.exit`, `POLL_CHUNK`).
- **`desk_stop {}`** → kills the session's runs and schedules the backend's idle stop (`SandboxBackend` already stops a Machine 3 min after its last exec).
  - It is also called automatically when the session ends, so a forgotten desk doesn't keep billing.

Each call logs an `agent.tool` event with the command (as desk tools do now), so the map and activity feed show "ran `npm test` at the desk".

Deliberately left out: `desk_read`, `desk_write` and `desk_edit`. `desk_run "cat …"` / `git diff` covers reading. Writing files remotely is how we'd end up rebuilding Claude Code over MCP (see Q2).

Good uses: `git log` or `git diff`, `npm run typecheck` / tests on main, `curl /api/health` + `git merge-base --is-ancestor` to check a deploy, and reproducing a bug before writing the assignment.

## 4. How a server session delegates real code changes

- **New verb `delegate {title, description, contextDocIds?}`.** It creates an assignment **for the caller itself** with `desk: true`. Today `assign` is managers/reviewers only, and that rule stays as it is.
  - The description gets the context doc ids appended (for a 1:1, the transcript doc).
  - It returns the assignment id.
- **Inside a work session**, the agent then parks with the mechanism we already have: `submit_report {resumeWhen: {assignment: <id>}, next: "…"}`.
  - The desk assignment runs, reports, and the server continuation resumes with that report as "your previous report".
  - Nothing new is needed for the wait.
- **Inside a 1:1 or meeting**, nothing parks. The desk assignment goes into the normal queue, and its report lands in the in-tray as usual.
- Reports remain the human interface (non-negotiable 1). The desk assignment always ends in its own report.

## 5. What changes in the runtime

1. **Backend per assignment, not per building.**
   - `startWork` in `runtime/src/index.ts` picks `runDeskSession` when `assignment.desk` is true, otherwise `runWorkSession`.
   - Drop the `codeWorkspace` refusal in `runWorkSession`. In code buildings, host sessions get the desk verbs instead.
2. **Schema and migration:** `assignments.desk INTEGER NOT NULL DEFAULT 0` (new `packages/core/migrations/NNN_assignment_desk.sql`), plus `desk?: boolean` on the `assign`/`delegate` inputs and meeting decisions. The mock server in `packages/web/src/mock/server.ts` needs the field too.
3. **`DeskBackend` gains `start(handle, command, env) → runId` and `poll(handle, runId, offset)`.**
   - Fly: move the background-launch and poll halves out of `FlyApi.run`. Today they live inside one function.
   - Docker: the same wrapper script through `docker exec -d`, and the poll is `docker exec … tail -c`.
   - `exec`/`run` (used by desk work sessions) then sit on top of start + poll.
4. **Desk CLI:** a `prepare` subcommand in `packages/desk` that runs only the workspace setup and prints `{cwd, branch, head}`.
5. **Lifecycle and slots.**
   - Map the open desk to the host session id in `Ctx` (like `ctx.live`). `runAgentSession`'s `finally` calls `desk_stop`.
   - `desks.maxRunning` today counts live work sessions, which would now include cheap host sessions. Split it into `maxSessions` (host) and `maxDesks` (desk work sessions plus open desk-tool desks).
6. **Prompts (`core`):** add a short block to the host system prompt in code buildings: "you have desk_start/run/output/stop for checks; for code changes call `delegate` and park on it". The desk work prompt stays as it is.
7. **Unchanged:** funding (`fundingFor`; desk_run spends no tokens), the report and review flow, redeploy drain (host sessions already count), and how a desk session publishes over `/mcp` ([dc_y3mqyi25lw](../../note/2026-10/2026-10-21-how-desk-agents-publish-docs-and-reports-to-the-to-mqyi25lw.md)).

Known gap: Fly bills Machine wall-clock time, and we don't record it today for desk sessions either. Desk-tool use would add short Machine runs to that untracked cost. I suggest logging the seconds per `desk_run` on the event so it can be counted later.

Rough size: items 1–2 are a small PR. Items 3–5 are the bulk, about one desk-session-sized change touching `fly.ts`, `backend.ts`, `sandbox.ts`, `index.ts` and the desk CLI, plus tests next to the existing backend tests. Item 6 is a prompt edit.

## 6. Questions for you

1. **Default for code buildings.** Should Workshop assignments default to `desk: true` for now, so nothing regresses, and flip to server-first once the desk verbs have been used for a week? Or should they be server-first now, with the assigner (facilitator/manager) setting `desk: true` for code changes? I recommend the first.
2. **Commits from desk_run.** `desk_run` is a shell, so a server session *can* `git commit && git push` with it. I can't see a clean way to block that. I propose allowing it, so a one-line fix doesn't need a whole desk session, and saying in the prompt that anything larger gets delegated. OK?
3. **Delegation resume.** Is park-and-resume on the desk assignment's report the behaviour you want for work sessions? The alternative is that the server session just ends and the desk report goes to the manager.
4. **1:1 escalation.** Should Sage's 1:1 (decision 1) use `delegate` for its "take this to my desk" button, or wait until this lands?
