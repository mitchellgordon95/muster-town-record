---
id: "dc_kw06vwoduk"
type: "report"
state: "building"
title: "Style-guide skill has the sheet rule; docs/ copy in PR #450, parked on its CI"
authorId: "ag_fecemm985x"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-14T10:03:10.205Z"
sessionId: "se_dzq81t5a23"
assignmentId: "as_myycwmcwmu"
costUsd: 1.1405939
tokens: 57030
turns: 18
createdAt: "2026-11-14T10:03:10.196Z"
updatedAt: "2026-11-14T10:03:10.205Z"
---
## What I did
I read the muster-style-guide skill ([dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)). Then I added the same rule to docs/architecture.md and opened PR #450: https://github.com/mitchellgordon95/agent-town/pull/450. I've parked the session until its CI finishes.

## Findings
- **The skill already has the rule.** Section 12, "Sidebars and sheets", was added by Kelly on 2026-11-06 (updatedAt 04:24Z). It names Mitchell's rule from mt_0n8ttf1bur and the rule of thumb ("if it has its own id and you would scroll it, it is a sheet"). It also covers the shared `Sheet`, `SheetView` and `SheetTabs` components, `InSheet`, `DocSheet` and `LinkSheet`. There is a matching Don't line in section 11. I did not need to message Kelly again.
- **The docs/ copy is in PR #450.** There is no separate UI conventions doc in docs/, so the rule went into docs/architecture.md, in the "Web client" section just before "Every panel is a place". It is one paragraph: what goes in a sidebar, what goes in a sheet, the rule of thumb, and the `Sheet` component and its options. It says not to write a second modal shell and points to the skill's section 12. I also added a log entry in docs/log.d.
- **Checks:** `npm run check --fast` passes (docs, deadcode, typecheck, tests, 50 s). At first, typecheck failed on `fast-check` because my desk's install was out of date; `npm install` fixed that. PR #450's CI check was pending when I parked.
- **The skill is a little behind the code.** Section 12 says decks still open in the side panel. Turning decks into sheets (decision 2 of [dc_ll4ap5di82](../../meeting-notes/2026-11/2026-11-05-1-1-mitchell-and-teo-notes-4ap5di82.md)) has not shipped, and that part is not on any key result.
- Once #450 merges, all five key results have evidence (topic page [dc_cfyhhhf9c0](../../wiki/2026-11/2026-11-05-sidebars-and-sheets-gr-4csjpgh346-yhhhf9c0.md)) and the grant can be closed.

## What I need from you
Nothing needed.
