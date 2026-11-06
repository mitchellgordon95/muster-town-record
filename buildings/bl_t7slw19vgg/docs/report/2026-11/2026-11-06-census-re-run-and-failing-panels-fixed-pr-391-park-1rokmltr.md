---
id: "dc_9r1rokmltr"
type: "report"
state: "building"
title: "Census re-run and failing panels fixed: PR #391 parked on CI (mock 82/82 rows pass)"
authorId: "ag_lblwzvr4x8"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Census now sees sheets; mock 82/82 and live preview all pass. Continuation as_1z7037va90 waits on PR #391 CI (mark ready + merge, then live census + crop for kr_p6l1w6tade)."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-06T04:59:45.476Z"
sessionId: "se_uk0d8z15g0"
assignmentId: "as_hp1g7x0slm"
costUsd: 3.8826466000000006
tokens: 194132
turns: 81
createdAt: "2026-11-06T04:59:29.027Z"
updatedAt: "2026-11-06T04:59:45.476Z"
---
## What I did
- Ran the disclosure census on live (acda269) and on the mock signed in as admin, both sizes. Then fixed every failing row in one PR: #391 (https://github.com/mitchellgordon95/muster-town/pull/391), head 271190a3, draft.
- Checks pass: typecheck, check:css (0 stray values) and the web tests (379/379).

## Findings
- **Census was blind to the new sheets.** On live, every grant, agent and doc hash showed "no panel", because those now open as centred sheets. The census now handles them like this:
  - A grant or agent link sheet counts like a side panel.
  - A doc sheet (an item opened from the library, an in-tray or a cabinet) is a document body, so it is excluded.
  - In-trays and cabinets are measured as their sidebar list. The output says so.
  - An agent's Talk timeline is chat, the same as a meeting transcript. Mitchell said chat is never folded, so its words and the links inside its lines are not counted.
  - Two new options, `--buildings=` and `--agents=`, let it measure more than one building and one agent on live.
- **Before → after on the mock (signed in):** 64/78 → **82/82** counted rows pass.
  - agent Assignments: 19 → 12
  - building Goals: 14 → 10
  - library Documents: 14 → 12
  - Town Hall in-tray: 14 → 12
  - planning Roles: 21 → under 12
  - planning Buildings: 210 → under 200 words
  - outbox Pending: 13 → 11
  - gr_ocean: 14 controls, gr_stress: 13 controls; both now pass
- **Live data, through a local preview of the branch:** every counted row passes.
  - Grants: gr_ukrou4zjha, gr_567tikzitl, gr_zak30564zh (358 → 170 words), gr_kvmwutmybu, gr_4csjpgh346 (205 → under 200 words).
  - Buildings: Onboarding, UI/UX, Workshop, Prod, all tabs.
  - Agents: Pix, Planner.
  - Before the fixes, the preview found three more fails:
    - Onboarding Goals: 213 words
    - UI/UX Grants: 208 words
    - Prod Schedule: 228 words
- **The fix pattern:** the first screen is a summary, and each row's actions sit behind that row's own fold, one click away:
  - A queued assignment's ▲▼, Start next and Cancel fold in with its description.
  - Goals has one shared "How to check and marks" fold; met and missed key results fold to a count; rows are clipped to one line.
  - The Grants tab links to the in-tray once per section instead of once per row.
  - Each Schedule row folds its details.
  - Library filters fold under one line; the list shows the newest 6, then "Show the other N".
  - The in-tray's Mine / All / Funded by me buttons became one select.
  - The outbox's Decline and Delete fold.
  - Each role gets one "Change holders" fold.
  - On a grant's page the decide form folds under "Decide"; Talk stays visible.
- **Untouched:** the Bank, the goal editor, the Sheet shell, chat transcripts.
- **Still to do:** the live census on the merge sha and the crop, so kr_p6l1w6tade is still at-risk until then. Topic page [dc_qswk18hm5y](../../wiki/2026-11/2026-11-04-progressive-disclosure-gl-1ds3wl2n78-wk18hm5y.md) is rewritten with the plan.

## What I need from you
Nothing needed.
