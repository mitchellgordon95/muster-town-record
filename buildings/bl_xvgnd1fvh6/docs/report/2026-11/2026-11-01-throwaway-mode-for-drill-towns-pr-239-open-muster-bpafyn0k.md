---
id: "dc_e4bpafyn0k"
type: "report"
state: "building"
title: "Throwaway mode for drill towns: PR #239 open (MUSTER_TOWN_RUNTIME=off); parked on its CI"
authorId: "ag_0vfuaaxco1"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. The continuation as_nfn8kskkb6 (waits {pr: 239}) already carries the plan: merge if green, check prod contains the sha, file ONE replacement drill request, rewrite dc_nh11dqbf19 + dc_ts7ulpuk5o, re-point as_v31d893zqr and as_6ruhd6l16h. No rollup yet: #28 waits for the 02:00 UTC lag sample and 02:40 export check."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T01:41:51.738Z"
sessionId: "se_4in9nbpcz3"
assignmentId: "as_iybdzfl6oq"
costUsd: 2.0640706
tokens: 103204
turns: 43
createdAt: "2026-11-01T01:41:43.364Z"
updatedAt: "2026-11-01T01:41:51.738Z"
---
## What I did
Built a throwaway mode for drill towns and opened draft PR #239 (https://github.com/mitchellgordon95/muster-town/pull/239), branched from main 139f587. The session is parked until #239's CI finishes.

## Findings
- **Switch:** `MUSTER_TOWN_RUNTIME=off`, read in new `packages/server/src/throwaway.ts`. It is named to match `MUSTER_TOWN_DIRECTORY=on|off`. Unset or `on` behaves as before. Any other value throws at boot, so a typo can't quietly start sessions.
- **When the var is off:**
  - The server skips `startRuntime` for the root app and for hosted runtimes: no sessions, desks, schedules or hourly export.
  - The boot log prints one line: `[server] runtime off (throwaway)…`.
  - The backup job is restore-only (`BackupJob.restoreOnly`): no timers, no boot catch-up, `run()` is a no-op, so nothing is uploaded or pruned.
  - The first-boot restore (`restoreOnFirstBoot`) still runs; that is the part the drill tests.
  - Health shows `throwaway: true` and `backup.mode: "restore-only"`. On every server `backup.mode` is now added, and muster.town's will read `"hourly"`.
- **Scripts:**
  - `deploy/recover.sh` (throwaway APP) and `scripts/backup/restore.sh` now deploy their drill apps with `--env MUSTER_TOWN_RUNTIME=off`.
  - The "gone before the top of the hour" caveat is removed from recover.sh's header and from README "Recover"/"Backups". The default destroy and the `--keep` manual-destroy line stay, because the drill town still accepts live login tokens.
  - README's stale "can neither spend tokens" claim for restore.sh is fixed.
  - `deploy/fly/throwaway.sh` is **deliberately not changed**, only commented. It boots a fresh town with no copy and an empty Bank, and its load tests measure the runtime tick.
- **Tests:**
  - A new describe in `test/backup.test.ts` checks:
    - the var parses as described;
    - `start` is never called when off;
    - the restore still brings back the copy;
    - the restore-only job arms 0 timers where the same job without the mode arms 2;
    - `run()` makes 0 S3 requests and leaves the bucket's 41 objects unchanged;
    - health keys appear only in throwaway mode.
  - The backup, monitor and health tests pass alone: 55 of 55.
  - The full local `check --fast` had 248 of 249 passing. The failure was around the existing worker-thread timing test (backup.test.ts:281, which measures main-thread timer gaps) during a 6-minute run on a busy desk. I only saw the tail of the output, so which assertion failed is unconfirmed. CI will settle it.
  - Typecheck is green.
  - shellcheck: recover.sh and restore.sh are clean; throwaway.sh has the same 6 warnings as on main.
  - recover.sh dry run shows `--env MUSTER_TOWN_RUNTIME=off` on the build line.
- No migration. This covers **step 1 of proposal gr_6qlj35wnh3**, so Mitchell can count it when he decides that proposal.

**Plan for the resume (pr 239):**
1. If CI is green: mark #239 ready, merge it, and let CI ship it. Note the merge sha.
2. Check that `prod` contains the merge sha (`git merge-base --is-ancestor <sha> origin/prod`). recover.sh builds from `BRANCH=prod` by default, so the request must say "prod/main ≥ <sha>".
3. File ONE `request_human` (kind other, location as in dc_647d9m37u2):
   - First line: ignore dc_647d9m37u2 and dc_y43rdv5zm7.
   - Body: dc_647d9m37u2's body minus "no Claude token" and the top-of-hour timing. Requires main/prod ≥ the merge sha.
   - Says the throwaway runs no sessions and never writes to the bucket (it shows `"throwaway": true` in health), but accepts live login tokens for its ~25 min (that fix is in gr_6qlj35wnh3).
   - Keeps the paste-back instructions.
4. Rewrite topic pages [dc_nh11dqbf19](../../wiki/2026-10/2026-10-31-recovery-from-a-dead-volume-11dqbf19.md) and [dc_ts7ulpuk5o](../../wiki/2026-10/2026-10-29-secrets-and-tokens-7ulpuk5o.md).
5. In the report, re-point as_v31d893zqr and the parked as_6ruhd6l16h to the new request id.

## What I need from you
Nothing needed.
