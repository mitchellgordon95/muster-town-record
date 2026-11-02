---
id: "dc_95442i9c4e"
type: "report"
state: "building"
title: "Stress test done: the prod box can run 6 desks at once safely (8 is the hard ceiling). I'd keep one box rather than split services for now"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "ok sure, 6 desks. go"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T20:36:57.679Z"
sessionId: "se_ihmdyqdjc5"
assignmentId: "as_m2vorqa3yz"
costUsd: 0.5331127999999999
tokens: 20797
turns: 18
createdAt: "2026-10-21T20:33:20.827Z"
updatedAt: "2026-10-21T20:36:57.679Z"
---
## What I did
- Picked up the stress runs from my cut-off session. They had finished N=1–6 and N=8 was still going. I waited for N=8, then cleaned up the test containers on muster-prod-1.
- Wrote up the results: [dc_vxgg8r55ha](../../note/2026-10/2026-10-21-stress-test-how-many-desks-muster-prod-1-ovh-d2-8-gg8r55ha.md).
- Checked the code for your other answers. Subscription-first funding with donated keys as fallback is already in place (`packages/desk/src/run.ts:46-79`), so prod needs no new API key. That supersedes the API-key line in my plan.

## Findings
**Stress test.** I ran N fake desks at once, each with the runtime's real limits (2 GB, 2 CPUs). Each desk did the heaviest job an agent does: typecheck, the 170 tests and the web build. The town server wasn't running during the test.

| desks | each desk's slowdown | runs/hour | lowest free RAM | OOM kills |
|---|---|---|---|---|
| 1 | 1.0x | 19.6 | 6.3 GB | 0 |
| 3 | 1.3x | 46 | 4.4 GB | 0 |
| 4 | 1.65x | 48 | 3.6 GB | 0 |
| 6 | 2.3x | 51 | 1.8 GB | 0 |
| 8 | 2.9x | 54 | **0.1 GB** | 0 |

- Each compiling desk peaks at about 0.9 GB (range 904–931 MB).
- The CPUs max out at 3–4 desks. Past that, each desk just runs slower.
- RAM is the hard wall: 8 desks compiling at once only just fit, before counting the town itself.
- Real desks mostly sit waiting on the model, using about 0.4 GB and almost no CPU. So 6 is a safe cap, not a tight one.
- **Recommendation:** `maxRunning` = 6, plus a 4 GB swap file as a cushion. I'll recheck with real session data after cutover.
- Not measured: whether your subscription's rate limit binds before the box does.

**Splitting into desk, town and UI services.** My recommendation is not now. Here's why:
- **UI:** it's a static build. The town server or Caddy serves it at almost no cost, so splitting it out gains nothing.
- **Town:** one process on SQLite, so it's single-writer and can't scale out anyway. It's also light.
- **Desks:** these are the only heavy part, and the only split worth doing later. A second box would also keep the agents' arbitrary shell commands away from the database and secrets.
  - The code is close to supporting it. Desks are started with the `docker` CLI, which can drive a remote Docker host.
  - The one change needed: desks reach the town at a hardcoded local address (`host.docker.internal`, set in `packages/runtime/src/desk/session.ts:83`). That would need to become a configurable town URL.
  - A second d2-8 costs about $26/mo, which takes us over the $50 budget.
  - The trigger to do it: the 6-desk cap is regularly full, or we want desks isolated before strangers donate keys.

**Next session:** I'll open the deploy PRs from the plan [dc_mltonxkizi](../../article/2026-10/2026-10-21-plan-deploying-muster-town-to-muster-prod-1-and-a-tonxkizi.md):
- a systemd service and Caddy config for the box, with the firewall rule and swap;
- a configurable redeploy branch;
- CI.

After those merge, I'll do the fresh test on the box and then migrate the Workshop.

## What I need from you
Nothing needed, unless you disagree with capping desks at 6 or with keeping everything on one box for now.

## Reply from Mitchell (2026-10-21 16:36)

ok sure, 6 desks. go

