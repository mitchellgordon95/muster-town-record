---
id: "dc_6jrfpvtei2"
type: "report"
state: "building"
title: "gr_f5bmciloqy rejected: no re-proposal until Mitchell picks a visitor shape (A/B/C in dc_04i3sll7q5, asked in the next rollup); Lena fixes the two shape-independent bugs as exploration (as_2cgt1jz405)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_04i3sll7q5","dc_hmypit6hi8","dc_evzrmyl3pp"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Agreed: no re-proposal until Mitchell picks a shape; the ask goes out as its own Needs line in rollup 22. Lena's two shape-independent fixes run as exploration (as_2cgt1jz405)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T18:28:30.367Z"
sessionId: "se_p1o91vh53b"
assignmentId: "as_9trc0hk3ag"
costUsd: 1.5953557999999999
tokens: 18767
turns: 14
createdAt: "2026-10-27T18:27:46.763Z"
updatedAt: "2026-10-27T18:28:30.367Z"
---
## What I did
Read Mitchell's note on gr_f5bmciloqy ("we need to iterate on this"), the proposal itself (GET /api/grants/gr_f5bmciloqy; it was shape C with an A fallback: starter brief, one offer from the outbox or a reading task, unhomed report to the Town Hall in-tray), the town hall notes ([dc_evzrmyl3pp](../../../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zrmyl3pp.md), decision 5: "I'm not sure what the right shape is"), and Lena's review "Visitor agents today" ([dc_04i3sll7q5](../../article/2026-10/2026-10-27-visitor-agents-today-i3sll7q5.md), report [dc_hmypit6hi8](2026-10-27-visitor-agents-today-dc-04i3sll7q5-a-visitor-is-mo-ypit6hi8.md)). Then decided, assigned one piece, and tried a one-line `say` to Mitchell (he was 2 tiles away but idle; only Lena heard it).

## Findings
- **Decision: do not re-propose yet.** The rejection is about the shape, not the token ask. Lena's review puts three shapes in front of Mitchell: A guest resident of a building the visitor picks (member role, manager's offers, reports to that manager); B its user's proxy, cleaned up (no building, reports to the user's own panel; the KR text would need rewording since "useful work" becomes "work its user asked for"); C town freelancer (a town task board; reports to the Town Hall in-tray or the posting building). Re-proposing before he picks repeats the rejected move. The ask "pick A, B, C or a mix" goes into my next rollup as its own Needs-from-Mitchell line (not buried under Shipped, the lesson from the memory retro). After his pick: reword kr_4li00ad46e if B, then `propose_grant` with findingsDocIds [dc_04i3sll7q5](../../article/2026-10/2026-10-27-visitor-agents-today-i3sll7q5.md) and [dc_gp9s9vi4vb](2026-10-27-objectives-and-kpis-design-pushed-to-main-6f023c4-9s9vi4vb.md).
- **Exploration assigned in the meantime: Lena as_2cgt1jz405** (lane exploration, kr_4li00ad46e, ~50k adjusted of today's 828,571 allowance, 304,777 spent). Two fixes Lena found that are wrong under every shape: (1) an unhomed visitor's `submit_report` is filed under town-hall (bench) or null (plaza) and shows in no in-tray, while the verb tells the agent "a human works it"; fix = Town Hall in-tray shows it as its own row kind, truthful verb reply, homed visitors unchanged; (2) POST /api/agents/visitors only requires a signed-in user while the panel requires town.interact; fix = the route requires it too. No brief, no offers, no task board: those depend on the shape. Queued behind her transcript store as_yr3dbbxk9j.
- Live usage so far (Lena): 3 visitor agents ever, all Mitchell's, 0 reports, 0 strangers, so nothing from visitors feeds the Join KPI yet.

## What I need from you
Nothing needed from the in-tray; the one human ask (Mitchell picks shape A, B or C in [dc_04i3sll7q5](../../article/2026-10/2026-10-27-visitor-agents-today-i3sll7q5.md)) goes out in the next rollup.
