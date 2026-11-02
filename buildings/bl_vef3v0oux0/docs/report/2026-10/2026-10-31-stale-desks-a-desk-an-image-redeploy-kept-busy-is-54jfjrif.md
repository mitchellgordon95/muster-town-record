---
id: "dc_yn54jfjrif"
type: "report"
state: "building"
title: "Stale desks: a desk an image redeploy kept busy is now recreated once its session ends (PR #139, main 305a6e2); live check pending"
authorId: "ag_s1fk1sqx0j"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #139 merged at 305a6e2 (migration 063 stale_desks, additive). The live check is already parked as as_cp0uofwyqz (waitFor deploy 305a6e2), so no new assignment. Rollup once that check passes."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T01:39:24.757Z"
sessionId: "se_mkkzygna18"
assignmentId: "as_6zlbr9d03p"
costUsd: 1.6134522999999996
tokens: 80673
turns: 32
createdAt: "2026-10-31T01:39:13.011Z"
updatedAt: "2026-10-31T01:39:24.757Z"
---
## What I did
- Shipped the fix Mitchell asked for in the 1:1 mt_cvxnqawx7h, using his second acceptable option: the image redeploy writes down which busy desks it skipped, and the desk is recreated once its session has ended. PR https://github.com/mitchellgordon95/muster-town/pull/139 is merged to main at **305a6e2**. CI passed (check job 2m12s), and CI redeploys the server.
- This is **Workshop runtime code**, which Pix should know about: `packages/runtime/src/index.ts` (in `recreateDesks` and the new `recreateStaleDesks`), `packages/runtime/src/desk/sandbox.ts`, migration `packages/core/migrations/063_stale_desks.sql` (adds a table, nothing else), and one sentence in the "Redeploy" section of docs/architecture.md.
- Tests: runtime 176/176, core 513/513, typecheck clean. Two new tests: one in adopt.test.ts (the desk is not removed while its adopted session runs, is removed after the session ends, and only once), one in sandbox.test.ts (`ensure` waits for a removal already in progress on the same desk).
- I did **not** call `redeploy image=true`. The change runs on the server only and the desk image did not change. An image redeploy now would run on the old server code, so it would neither record nor recreate anything. It is the test, and it belongs to the next session.

## Findings
- **Why the record has to be in the database:** a desk that is busy during an image redeploy is always running a session that the *next* server adopts, because the redeploy restarts the server right after recreating the idle desks. A list kept in memory would be lost in that restart. So `recreateDesks` now empties a new `stale_desks` table and writes in every desk it keeps busy: a resident's own desk by agent id, a fork's desk slot by its sandbox name.
- **The watch:** at the start of every scheduler pass, `recreateStaleDesks()` takes each listed desk that has no session running or starting on it, deletes its row, and removes its Machine. The home volume stays. The next session's existing `ensure` then creates a fresh Machine from the new image.
  - A resident is held from starting a session until the removal finishes, the same way it is held while an orphaned session is being killed.
  - For fork slots, `SandboxBackend.ensure` waits for a removal in progress on the same name.
  - The session-start path makes no new API calls, and a running session is never touched. The desk posts session-end as its very last step, so removing the Machine after that cuts nothing short.
- **Known gaps (not fixed here):**
  - Docker-host desks (not Fly) still only remove the idle ones.
  - Fly can list a Machine as still being destroyed for a moment after the delete call returns. `ensure` already replaces a desk in an error state, but a desk caught at that moment could fail to start one session.
  - An adopted desk that is *not* on the old image is never stopped after its session ends: the new server has no idle-stop timer for it. Only the Machine's 6-hour lifetime limit stops it.
- **How to check it live (the next session, parked on deploy 305a6e2):**
  1. From a desk session, call `redeploy image=true`. That desk is busy, so it is kept.
  2. After the restart, `stale_desks` should list that desk.
  3. When the session ends, a system event "Recreating <name>'s desk on the new desk image…" (payload `staleDesk`) should appear, and the desk's Fly Machine id should be different from before.
- Topic page: [Stale desks after an image redeploy](../../wiki/2026-10/2026-10-31-stale-desks-after-an-image-redeploy-stale-desks-nuz69xpm.md).

## What I need from you
Nothing needed.
