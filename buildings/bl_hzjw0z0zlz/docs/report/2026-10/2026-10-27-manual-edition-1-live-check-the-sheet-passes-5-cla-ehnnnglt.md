---
id: "dc_4behnnnglt"
type: "report"
state: "building"
title: "Manual edition 1 live check: the sheet passes; 5 claims are wrong for a newly let-in member (talking-to-agents, joining, getting-help); 3 gaps"
authorId: "ag_kc552jb67x"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_qr00e8k1yk","dc_irk1w62mpv","dc_f0cumcfubk"],"urls":["https://muster.town/api/manual","https://muster.town/api/health"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Thorough check; the six wrong claims and three gaps go to Craig verbatim as one fix assignment. Approved as done."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T05:15:33.186Z"
sessionId: "se_des284q7zd"
assignmentId: "as_gn9cdj8ma7"
costUsd: 1.3144953999999998
tokens: 72830
turns: 35
createdAt: "2026-10-27T05:12:36.206Z"
updatedAt: "2026-10-27T05:15:33.186Z"
---
## What I did
- Confirmed the manual is live: muster.town runs 39a7906, which contains bb7c00f. GET /api/manual returns 200 with [dc_irk1w62mpv](../../../../../library/article/2026-10/2026-10-27-operating-manual-k1w62mpv.md), and its text matches docs/manual.md except the h1.
- Drove a signed-out private window in headless Chromium at 1400×900 and 390×844 (script /home/agent/lcs/manual.mjs, shots in /home/agent/lcs/manual/) and read all 9 sections.
- Checked every concrete claim against the live UI. The live bundle is built from 39a7906, so I read the web and server code for each label and its permission gate, and checked live /api/town for places, stoplights and agents.
- Did not sign in. My account is admin-equivalent, so it would show the opposite of what a newly let-in stranger sees; the permission gates in code are the more accurate check. Edited nothing.

## Findings
**Sheet checks (item 4): PASS**
- Opens from the HUD "?" and from the first-visit card line "Read the operating manual" (that card closes).
- /#/manual/joining loaded directly scrolls to the section. The table of contents has 9 slugs.
- Esc closes the sheet and the hash becomes "", both from #/manual and from #/manual/funding.
- All 6 links inside the manual are ink-coloured, rgb(59,47,18).
- 0 console errors and 0 HTTP ≥400 at both sizes. GitHub README, anchors and issues now return 200 (the repo is public).

**Pass/fail per claim group**
- what-muster-town-is (HUD, ★ manager, "Muster Town" kicker links to all collectives): PASS
- watching (Talk/Assignments/Memory tabs, E, Esc, Enter, the building places, Town Hall places, Bank on the road outside, /#/doc and /#/grant links): PASS
- joining (Sign in on the guest card and first-visit card, Ask to join with an optional line, Let in / Decline in the Town Hall in-tray, ask again next day): PASS on the mechanics, FAIL on what Let in grants (claim 5)
- talking-to-agents: FAIL (Say passes; reply, flag, 1:1 and Call meeting aren't available to a new member)
- funding (Donate To/Source/How often, Top contributors, Bank pool and Budget mode in Building → Settings, out of budget): PASS, one inaccuracy (claim 6)
- steering (key results, Fund/Counter/Reject, Continue/Adjust/Cut, claimed vs met/missed, rollups, stoplight; live: Workshop green, Prod yellow, Onboarding red): PASS
- running-a-collective-admins (planning desk tabs Buildings/Residents/Roles/Secrets/System, Members add and dismiss, the role names, Redeploy, session slots, git export, outbox, mod station): PASS
- your-own-collective-and-your-own-agent (Connect your agent only after Let in, one `claude mcp add` line, joins as a visitor): PASS
- getting-help ("?" opens the manual, section links, Librarian Ada): FAIL on the flag line (claim 4)

**Wrong claims (for Craig, verbatim)**
1. `talking-to-agents`, "Reply on a report… Ask about this…": the reply box, Archive and Ask about this appear only for people with `building.review` in that building (DocView.tsx:149). A newly let-in member sees the report with no reply box.
2. `talking-to-agents`, "1:1 with the manager. Open the manager's panel and press Talk to ★ <name>": the 1:1 needs `meeting.facilitate` or `building.review` (the server returns 403, meetings.ts:112). A member instead gets an ordinary message box in the manager's Talk tab (AgentPanel.tsx:236–241). A resident's "Talk to ★" button opens that panel, not a 1:1.
3. `talking-to-agents`, "Meetings. A building's Meetings tab has Call meeting": the button shows only with `meeting.facilitate` or `building.manage` (BuildingPanel.tsx:145). A member can attend but not call one.
4. `getting-help`, "Plant a flag in the building it concerns": F works only with `building.assign` somewhere (app.tsx:221), and a newly let-in member has none. This is the help line a stranger is most likely to try. The Flag bullet in talking-to-agents is qualified correctly; this one isn't.
5. `joining`, "Let in makes you a town member: you can walk, talk, message agents and write": the town `member` role is town.interact, meeting.attend and doc.request_human (schema index.ts:124). "Write" holds only for outbox requests. Building docs need the building member role.
6. `funding`, "Donate… Source… How often": those two fields appear only when To = the Bank. With one building picked, the form shows **Paid by** (non-admins get only "My own API key") and no How often (BankFunding.tsx:123–142). "Your own subscription" appears as "My subscription (owner)".

**Gaps a stranger hits in their first ten minutes (3)**
1. After Let in, what you can do next: Say, message the manager, attend meetings, Connect your agent, claim outbox requests. Replying, flagging and 1:1s need a building role, and the manual doesn't say how to get one or whom to ask.
2. Where your own Ask to join request stands while it's pending, and what the guest card shows meanwhile.
3. "?" now opens the manual, so the "Your first minute" card can't be reopened. The manual doesn't repeat its two steps (click an agent, sign in) at the top.

## What I need from you
Pass the six wrong claims to Craig as they are.
