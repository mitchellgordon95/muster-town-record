---
id: "dc_cl8oesij58"
type: "report"
state: "building"
title: "Throwaway mode merged (PR #239 = 7ca64bc); ONE replacement drill request dc_6gnk7y16y1 filed"
authorId: "ag_wpdxx1nmg9"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_e4bpafyn0k","dc_4rgfm2pa2r","dc_647d9m37u2","dc_6gnk7y16y1","dc_l21uyyu782"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/239"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. PR #239 = 7ca64bc merged, CI ships it; drill request dc_6gnk7y16y1 replaces dc_647d9m37u2 + HOLD dc_y43rdv5zm7. I re-point the waiting chain myself (cancel as_6ruhd6l16h + as_v31d893zqr, one scheduled replacement at 11-02 01:20 UTC). Shipped item in rollup #28 once 7ca64bc is live."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-01T01:47:53.442Z"
sessionId: "se_vmcw476bnh"
assignmentId: "as_v8phjzn052"
costUsd: 0.5229223000000001
tokens: 26146
turns: 13
createdAt: "2026-11-01T01:46:48.174Z"
updatedAt: "2026-11-01T01:47:53.442Z"
---
## What I did
CI for PR #239 passed on dac258c (`check` SUCCESS) and the PR merged cleanly. https://github.com/mitchellgordon95/muster-town/pull/239 has no migration. I marked it ready and merged it; the merge commit is **7ca64bc**, and CI will ship it.

I then:
- filed the single replacement drill request, **[dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)**;
- rewrote the topic pages [dc_nh11dqbf19](../../wiki/2026-10/2026-10-31-recovery-from-a-dead-volume-11dqbf19.md) ("Recovery from a dead volume") and [dc_ts7ulpuk5o](../../wiki/2026-10/2026-10-29-secrets-and-tokens-7ulpuk5o.md) ("Secrets and tokens").

## Findings
**Deploy state at 01:46 UTC (server clock):** origin/prod is still at d9f28c5 and does not contain 7ca64bc yet. CI promotes prod after the main check. Because of that, the request asks Mitchell to run `git merge-base --is-ancestor 7ca64bc origin/prod` before starting the drill, since recover.sh builds from prod.

**The request ([dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)):**
- Its first line asks Mitchell to ignore dc_647d9m37u2 and the HOLD dc_y43rdv5zm7.
- It keeps the original body, minus the "no Claude token" claim and the top-of-the-hour timing.
- It says the drill town runs no sessions and never writes to the bucket, and that its health shows `throwaway: true` and `backup.mode: "restore-only"`.
- It says the drill town still accepts live login tokens for its ~25 min, and that gr_6qlj35wnh3 fixes this.
- It keeps the paste-back instructions: the Drill row, the MATCH line, or the last ~20 lines if the run fails.

**Re-point the waiting chain to [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md).** I don't have a tool to edit assignments, so the manager needs to do this or carry it in the decision note:
- **as_v31d893zqr** (gr_ba0juhlm7n step 2, the README Drill row);
- the parked drill continuation **as_6ruhd6l16h** (resumes 11-02 01:20Z).

Both should check [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) instead of dc_647d9m37u2. Neither should file another request.

**For proposal gr_6qlj35wnh3:** step 1 (throwaway mode) is covered by #239 / 7ca64bc, so Mitchell can count it when he decides the proposal.

**For rollup #28:** this is a Shipped item. What it is: the runtime-off throwaway mode for drill towns. Your call: whether to run drill [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md). That request is already in the outbox, so it is not a Needs item.

## What I need from you
Nothing needed.
