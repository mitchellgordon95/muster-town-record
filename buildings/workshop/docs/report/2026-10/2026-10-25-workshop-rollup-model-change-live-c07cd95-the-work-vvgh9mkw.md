---
id: "dc_zgvvgh9mkw"
type: "report"
state: "building"
title: "Workshop rollup: model change live (c07cd95), the Workshop is now correctly blocked; three draft key results for Mitchell to write or negotiate"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_h2v9eyyrhh"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": The open Workshop grant proposal gr_jqsqra0dlx predates c07cd95 and names no key result, so it is out of date in form. Mitchell writes the Workshop's key result"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-25T18:54:03.342Z"
sessionId: "se_8fgxk03lvc"
assignmentId: "as_miipsnyz5p"
createdAt: "2026-10-25T18:44:18.076Z"
updatedAt: "2026-10-25T18:54:03.342Z"
---
## Shipped
- **c07cd95** (Lena, [dc_h2v9eyyrhh](2026-10-25-model-change-core-pushed-to-main-c07cd95-krs-on-th-v9eyyrhh.md)), live: the model change you asked for in our 1:1s ([dc_bo7xuobtbv](../../meeting-notes/2026-10/2026-10-25-1-1-mitchell-and-pix-notes-7xuobtbv.md), [dc_vaaqyc943b](../../meeting-notes/2026-10/2026-10-25-1-1-mitchell-and-pix-notes-aqyc943b.md)). Key results live on the building goal and only a human writes them; a grant names one key result and carries its plan, its old key results became a testing plan (migration 032); a goal-directed building with no key results and no funded grant shows "blocked: no key results to work toward" and wakes its manager once. That wake fired for the Workshop at 18:41Z, which is why this rollup exists.
- In flight, no decision needed: Root builds the UI (key-result editor in Building → Settings, grant forms pick a key result, blocked badge; as_tatcakwm1m). Keel makes meetings survive a redeploy (as_tmqcmufeup).

## Decided
- [dc_h2v9eyyrhh](2026-10-25-model-change-core-pushed-to-main-c07cd95-krs-on-th-v9eyyrhh.md) (Lena, parked for the live check) → approved; the live check runs by itself.

## Key results
The goal "Ship improvements to Muster Town's core experience" has none yet, so the Workshop is blocked. No funded grant. Exploration today: 10.1M of the 4M-token allowance (Lena's core session cost 8.3M), so Root's and Keel's exploration work is held until the allowance resets or a grant is funded.

Draft key results, each checkable in the live town. You said you'd rather negotiate these in conversation than counter a draft, so treat them as the opening of that conversation:

1. **The Workshop never stalls silently.** At any moment it either has work in flight toward a key result, or shows exactly one blocker and what unblocks it. Funding a grant, deciding a checkpoint or writing a key result starts work within one session cycle, with no meeting and no poke from you. How to check: open the Workshop at a random time; then fund or cut a grant and watch the assignment or the blocker appear.
2. **You steer from the Town Hall in-tray alone.** Every decision you have to make (proposal, checkpoint, rollup, blocked building) reaches you there, and nothing in the town needs a direct message from you to move. How to check: over 24 h, every decision you made was in the in-tray and its badge count was right; no `tell` or 1:1 was the only way to unblock something.
3. **A redeploy loses nothing.** Parked sessions resume once, meetings continue with a transcript line saying the reply waited on the restart, and no duplicate sessions appear. How to check: redeploy during a meeting and during a work session; both continue and nothing runs twice.

The open proposal gr_jqsqra0dlx (24M tokens, "the Workshop runs itself") maps onto key result 1; its three former key results are already its testing plan. Once key result 1 exists I point the grant at it and re-propose under the same id, so Keel's, Lena's and Root's held work starts on funding.

## Needs from Mitchell
1. Write key results on the Workshop goal (Building → Settings → Key results, once Root's UI lands; until then tell me what to change or open a 1:1), starting from the three drafts above.
2. After that, fund gr_jqsqra0dlx (re-proposed against key result 1), or raise the Workshop's exploration tokens/day, so Root's UI and Keel's meeting fix can run today instead of waiting for the allowance to reset.
