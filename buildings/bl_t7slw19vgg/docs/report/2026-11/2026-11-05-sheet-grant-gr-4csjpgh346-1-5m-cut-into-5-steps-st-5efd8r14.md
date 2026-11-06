---
id: "dc_ep5efd8r14"
type: "report"
state: "building"
title: "Sheet grant gr_4csjpgh346 (1.5M) cut into 5 steps; step 1 (one shared Sheet component, Bank + goal editor on it) queued as as_xapgn49yfp; style-guide wording sent to Kelly"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_ll4ap5di82","dc_cfyhhhf9c0"],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Plan stands as written: step 1 runs as as_xapgn49yfp; steps 2-5 queue one at a time when step 1's report lands. Step 5's check of Kelly's skill goes on the schedule for the 14th."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-05T20:31:17.758Z"
sessionId: "se_sv4htlvut4"
assignmentId: "as_e08ausklg7"
costUsd: 1.7977553
tokens: 89888
turns: 15
createdAt: "2026-11-05T20:31:01.048Z"
updatedAt: "2026-11-05T20:31:17.758Z"
---
## What I did
Read the 1:1 notes ([dc_ll4ap5di82](../../meeting-notes/2026-11/2026-11-05-1-1-mitchell-and-teo-notes-4ap5di82.md)) and the two centred shells in the code, wrote the grant's topic page "Sidebars and sheets (gr_4csjpgh346)" ([dc_cfyhhhf9c0](../../wiki/2026-11/2026-11-05-sidebars-and-sheets-gr-4csjpgh346-yhhhf9c0.md)) with the rule, what exists today and the five steps, queued step 1 on the building queue in lane grant, and sent Kelly (Onboarding) the wording for the style-guide section the last key result needs.

## Findings
Mitchell funded gr_4csjpgh346 at 1,500,000 tokens (the ask was 900,000). The plan cuts into one session per step; each step's check is the key result's own.

- **Step 1, queued now (as_xapgn49yfp, kr_xnt1h13yce, due 2026-11-09):** one `Sheet` component (packages/web/src/panels/Sheet.tsx, `.sheet-*` CSS: head, optional left tabs, main, optional side with the resizable divider, full screen on a phone), with the Bank (BankSheet.tsx, `.bank-*` at styles.css:959, copied from the goal editor per its own comment) and the goal editor (GoalTreePanel.tsx, `.ge-*` at styles.css:861) both on it. Check: before/after crops at 1280×800 and 390×844 in the mock, then on live; git grep shows the two shells gone. Topic pages attached: [dc_cfyhhhf9c0](../../wiki/2026-11/2026-11-05-sidebars-and-sheets-gr-4csjpgh346-yhhhf9c0.md) and the Bank interior page [dc_v4itjbkgfi](../../wiki/2026-10/2026-10-30-bank-interior-tabs-and-room-objects-itjbkgfi.md).
- **Step 2 (kr_gg1wjnt07k, due 11-12):** Town Hall in-tray and filing cabinet keep the list in the sidebar; a report, proposal or checkpoint opens as a Sheet with its Your-call block and decide buttons. Queued once step 1 is merged.
- **Step 3 (kr_sa1gn36ndz, due 11-14):** docs, grants, agents from links open as a Sheet; decks too (per decision 2 of the 1:1). Likely two sessions.
- **Step 4 (kr_pm0fmsiaxs, due 11-16):** wider sanitizer allowlist (can run beside step 2), then doc type "page" in a sandboxed iframe with a sample chart page in the library.
- **Step 5 (kr_nokx342ovj, due 11-16):** the rule in Kelly's muster-style-guide skill [dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md) and docs/. Wording sent to Kelly (ms_o6m1ql4sde); she is idle, so I check the skill around the 14th and queue the docs/ copy then.

The queue also holds as_xryg315zhb (PR #368 bulletin read/unread, waiting on CI) and as_49mgtd5x7v (PR #350, held by gr_kvmwutmybu's checkpoint); neither blocks step 1.

## What I need from you
Nothing needed.
