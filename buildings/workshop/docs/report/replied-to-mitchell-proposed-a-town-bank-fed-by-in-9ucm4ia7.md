---
id: "dc_y89ucm4ia7"
type: "report"
state: "building"
title: "Replied to Mitchell: proposed a town Bank fed by inputs, split to buildings by %"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T16:29:49.697Z"
sessionId: "se_x645cyepa7"
assignmentId: "as_bfwehrueqm"
costUsd: 0.19418939999999998
tokens: 142022
turns: 8
createdAt: "2026-10-20T16:26:17.308Z"
updatedAt: "2026-10-20T16:29:49.697Z"
---
## What I did
Read Mitchell's message and Pix's budget report (dc_rydi7dslzp), and checked `packages/core/src/budget.ts` on main (c8b8c17). Then replied to Mitchell with a design. No code changed.

## Findings
- **Today's code:** money comes in as user donations. Each donation becomes an allocation to a single building and can carry the donor's API key (`apiKeyFor`). There is no town-level balance.
- **Proposal sent to Mitchell:**
  - **Town Bank:** lives in Town Hall and is fed by inputs. Each input is {API key or subscription, model, tokens, one-time or recurring with a period and next renewal}.
  - **Crediting:** a one-time input credits once. A recurring input credits only on its renewal date.
  - **Subscriptions:** only Mitchell's own subscription can be an input, since pooling other people's subscriptions would break Anthropic's terms. It credits min(daily quota, remaining weekly cap) each day.
  - **Buildings:** each building gets a % share of inflow and no longer refreshes daily. Any unassigned share stays in the Bank as reserve.
  - **Bank view:** lists inputs, balance, daily inflow and building shares.
- **Build order proposed:** (1) inputs + Bank balance, (2) the % split, (3) the Town Hall view. I'm waiting for Mitchell to confirm before building.

## What I need from you
Nothing needed.
