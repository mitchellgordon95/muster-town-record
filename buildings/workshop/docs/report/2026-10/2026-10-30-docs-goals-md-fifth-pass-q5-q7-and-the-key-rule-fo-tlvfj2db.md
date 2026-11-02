---
id: "dc_vptlvfj2db"
type: "report"
state: "building"
title: "docs/goals.md fifth pass: Q5-Q7 and the key rule folded in, all 1:1 questions closed; PR #116 head bb3c3e0 (not merged)"
authorId: "ag_brm30n4l7u"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #116 at bb3c3e0: all 1:1 mt_kh0zaqui0w questions folded in; Mitchell waived the final read (\"we're good\"). Build step 1 as_6zx9zmtvdo starts now (it merges PR #116 first)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T20:32:13.022Z"
sessionId: "se_dx5voepoje"
assignmentId: "as_3chyvmzlf8"
costUsd: 0.7153722000000001
tokens: 35769
turns: 12
createdAt: "2026-10-30T20:32:07.461Z"
updatedAt: "2026-10-30T20:32:13.022Z"
---
## What I did
Folded Mitchell's remaining answers from 1:1 mt_kh0zaqui0w into docs/goals.md on the PR #116 branch. This change touches docs only. Commit bb3c3e0 is pushed and visible on origin (agent/pix-2/design-doc-docs-goals-md-town-level-goal). It is not merged. https://github.com/mitchellgordon95/muster-town/pull/116. I also rewrote topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md).

## Findings
- **Owners (Q5):** an owner can now decide **and fund** grants in their subtree, through `building.fund` scoped to that subtree. Funding is no longer limited to admins. Member funding (kr_6f9c200vsx) is unchanged. Owners are humans only for now, and managers propose. Build step 4 adds a Fund button for owners in the in-tray.
- **Reorg timing (Q6):** "Change this goal" no longer asks for a meeting date. The meeting opens when every attached building's prep report is in, or 24 h after the change is filed, whichever comes first. A goal with no attached buildings opens its meeting at once. Grants keep running throughout. In `goal_changes`, `meetingAt` is now `meetingDeadline`, and the status values are now `prep | meeting | decided`.
- **Skip-level (Q7):** dropped. The section is down to one line that keeps it as a possible later addition, along with the conversational fork session. I also removed it from the editor tabs, the meeting uses, the UI inventory and the build order.
- **Keys:** the one-key-per-session rule is confirmed. A key whose daily limit is below one session's expected cost (the building's p90 over 7 days) never runs a session alone; it saves up until it can cover one. I added two things:
  - a warning on the Donate form: "your key covers no whole session yet";
  - an alert when a donation goes 7 days without being used. The donor gets an in-town notice and the funder's deck gets a line. Any email or SMS goes through Wright's VPS pinger, not the server (c45eaeb).
  
  Both are now part of build step 7 and the Bank panel row of the UI inventory.
- **Build order:** renumbered to 8 steps. Steps 7 (streams and draw order) and 8 (funder filter) are the Bank-gated ones. I updated every cross-reference to them in the finance section, the "what changes" list and the UI inventory. I also fixed the stale "Planner: who pays is open question 1" line: it now says draw order, per mt_529jbnwvmi.
- **Open questions:** only the two map questions remain (what an empty goal looks like, and long walks on deep trees). Everything else is struck through, with its answer.
- **Next:** the doc is ready for Mitchell's final read. Build step 1 can be queued as directed work with sourceId mt_kh0zaqui0w. Steps 7 and 8 still need his yes on the code.

## What I need from you
Nothing needed.
