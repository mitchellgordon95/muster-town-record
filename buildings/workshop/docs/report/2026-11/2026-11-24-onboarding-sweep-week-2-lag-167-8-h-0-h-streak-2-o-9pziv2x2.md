---
id: "dc_2x9pziv2x2"
type: "report"
state: "building"
title: "Onboarding sweep week 2: lag 167.8 h → 0 h, streak 2 of 4; PR #587 merging on green"
authorId: "ag_oiey4i6jvs"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-24T19:14:05.781Z"
sessionId: "se_85244hpujh"
assignmentId: "as_wj99cix2m8"
costUsd: 1.448229
tokens: 72411
turns: 28
createdAt: "2026-11-24T19:14:05.766Z"
updatedAt: "2026-11-24T19:14:05.781Z"
---
Lag 167.8 h at start (under the 168 h line by 0.2 h), 0 h after; streak 2 of 4 weekly sweeps.

## What I did
Swept the 87 commits from 67dd6a73 to 0c51d5a3 against the onboarding materials, using skill [dc_kzuf6rx4la](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-29-onboarding-staleness-sweep-2-uf6rx4la.md). Fixed what was stale in PR https://github.com/mitchellgordon95/muster-town/pull/587. `npm run check -- --fast` passed locally (1m55s). Rewrote topic page [dc_t4jw2xcwut](../../wiki/2026-10/2026-10-31-onboarding-lag-gr-mjr7nb438v-jw2xcwut.md) and told Kelly.

## Findings
- **2 stale claims and 1 gap fixed.**
  - The manual pointed to the goal's "Funding" for the explorer chunk. That label is now "Exploration and money settings" (GoalTreePanel.tsx:347).
  - SKILL.md still listed the `redeploy` verb, which was retired in #498.
  - Gap: SKILL.md's resumeWhen list now includes `{deploy, checks}` (#552) and `{pr, merge: true}` (#512).
- **Manual length:** 1891 words. I trimmed one filler line under Steering to stay under the 1900 cap.
- **Checked and not stale:** objectives being removed (#506), captains deciding asks in their subtree (#534), ask buttons that act (#555), and the admin Redeploy in README and manual (that admin route still exists).
- **Checked-through sha: 0c51d5a3.** `scripts/onboarding-lag.sh 0c51d5a3` gives 0 h.
- **Risk:** each sweep starts from the last sweep's main head, so a 168 h schedule lands right at the line. This week was 0.2 h from a miss. Moving sc_fcj3l0szia a few hours earlier would give some margin.
- The old branch name already existed on origin, so I pushed to a new branch, agent/pix-1/onboarding-sweep-week-2, without force-pushing.

## What I need from you
Nothing needed.
