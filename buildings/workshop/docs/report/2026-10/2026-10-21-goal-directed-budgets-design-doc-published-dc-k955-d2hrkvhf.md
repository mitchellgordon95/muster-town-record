---
id: "dc_r3d2hrkvhf"
type: "report"
state: "building"
title: "Goal-directed budgets design doc published (dc_k955hun6c4) and shared with Mitchell"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "i'll read the doc, but while i'm doing that can you build doc links so reports can link to docs etc.?\n\nif we don't already, we should have a reasonable filesystem architecture for all this stuff we're generating that will stay legible and scale"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T01:24:49.385Z"
sessionId: "se_1ikz3zr3oc"
assignmentId: "as_nirhmeorqh"
costUsd: 1.2939349999999998
tokens: 63524
turns: 35
createdAt: "2026-10-21T01:21:15.568Z"
updatedAt: "2026-10-21T01:24:49.385Z"
---
## What I did
I read the budget, Bank, board, assignment, permission and desk-brief code, and pulled live Bank and session-spend numbers. Then I wrote the design doc and committed it to main as `docs/goal-directed-budgets.md` (d7acaea, plus a wording fix in b97fe7c), with a line in docs/log.md. It is published in the Workshop filing cabinet as **[dc_k955hun6c4](../../article/2026-10/2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md)**. I sent Mitchell a message and started a redeploy. Nothing is built yet.

## Findings
- **Flow:** a goal-scoped exploration allowance, then the manager's building proposal (objective, 2-3 human-observable key results each with a "how to check" line, token ask, stop condition), then a human funds, counters or rejects it, then agents work freely inside the funded grant. At 50% spend, new sessions on the grant are held and the manager writes a checkpoint; the human continues, adjusts or cuts. Only a human can mark a key result met or missed; the manager can at most mark it "claimed".
- **Three spend lanes per assignment:** grant, exploration (has to name a key result or a goal gap) and directed (created by a human). Agents can't create directed work. They are enforced in the one existing gate, `Budget.canStart`, which becomes `canStart(agent, assignment)`. Spend per grant and per day of exploration is derived from session tokens rather than kept in a second counter.
- **Data model:** new `Grant` and `KeyResult` tables. New fields: lane, grantId, keyResultId and gap on Assignment and Session; explorationTokensPerDay and budgetMode on Building. New permission `building.fund`, which is never effective for agents. Without that, an agent manager whose owner is an admin could fund its own proposal.
- **API, UI and rollout:** the API is `GET /api/buildings/:id/board`, grant CRUD, propose and decide; agents get the MCP verbs `propose_grant` and `checkpoint_grant`. The Board panel is reworked as goal, then key-result cards with spend bars and a 50% tick, then the open proposal with Fund / Counter / Reject, then the exploration meter, then rules, then FYIs. The desk brief gets a Key results block, because today it only tells agents to look at the board. Rollout is behind `budgetMode` (default `open`), with the Workshop as the pilot.
- **Sizes:** the live pool takes in 20,000,000 tokens/day, and a Workshop session costs a median of about 950,000 tokens (range 210,000 to 10,600,000, n=38). So 10% split across the three drawing buildings would give about 670,000 tokens/day each, less than one session. I proposed 10% per building instead, which is 2,000,000 tokens/day each.

## What I need from you
Mitchell: read [dc_k955hun6c4](../../article/2026-10/2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md) and answer its four open questions: exploration size (per building or split), whether directed work bypasses grants, who can fund, and grants as ceilings or reservations. After that I can assign the build.

## Reply from Mitchell (2026-10-20 21:24)

i'll read the doc, but while i'm doing that can you build doc links so reports can link to docs etc.?

if we don't already, we should have a reasonable filesystem architecture for all this stuff we're generating that will stay legible and scale

