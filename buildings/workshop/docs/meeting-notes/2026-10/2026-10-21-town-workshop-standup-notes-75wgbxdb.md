---
id: "dc_jx75wgbxdb"
type: "meeting-notes"
state: "building"
title: "Town Workshop standup — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-21T01:38:34.431Z"
updatedAt: "2026-10-21T01:38:34.431Z"
---
# Town Workshop standup

Kind: standup. Facilitator: Pix. Attendees: Lena, Pix, Root, Sage.

## Agenda

(none)

## Summaries

**Pix:** Did: I wrote and published the goal-directed budgets design doc, then sent it to Mitchell for review.
Next: I'll add doc links for reports and sketch a filesystem layout for the docs we generate.
Need: Mitchell, please answer the four open questions in the design doc so I can start the build.
**Root:** Did: I confirmed the live server returns per-building token counts for today and all-time, and I made no code changes.
Next: I'll confirm the live server has the newest fix, then check the building panel and banner.
**Sage:** Did: I verified the building banners work live, including the full goal text and clicking to open.
Next: I'm sending a request for a manager to click a banner and confirm the Settings tab opens.
Need: A GitHub manager needs to sign in and click a banner on a building they manage.
**Lena:** Did: I finished the accounting pools web half and pushed the token usage panel to main, then redeployed.
Next: Once Root's live check passes, I'll file the close-out report and fix anything Root finds.

## Discussion

- **Pix:** Agenda: 1) Token usage panel: Root's live check of the building panel and banner, then Lena closes out. 2) Banners: Sage needs a GitHub manager to click one and confirm the Settings tab opens. 3) Budgets design doc: waiting on Mitchell's answers to 4 open questions. Meanwhile Pix works on doc links and the docs filesystem layout.
- **Mitchell:** for sage, yes it works but i think we should change it to the Overview tab

what are the budget questions?

and then i need someone to figure out a skill system so agents can add and share skills (i have a personal one i want to add to this town in particular)
- **Pix:** Mitchell, noted: Sage will change the banner click to open Overview instead of Settings. The budget questions (doc [dc_k955hun6c4](../../article/2026-10/2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md)), each with my default:
1) Exploration allowance: 10% of the pool's daily inflow for each building (2M tokens/day each), or split across buildings (~670K each, under one median session)? Default: per building.
2) Directed work: should tasks a human assigns directly keep bypassing grants? Default: yes.
3) Who can fund grants: only town admins, or also humans with a building's manager role? Default: both.
4) Grants: spending ceilings, or hard reservations carved out of the pool? Default: ceilings.
A short "defaults ok" is enough, or override any of them. On skills: I'll take the design. Plan: a skill is a markdown doc agents can publish and share in the library, and buildings can pin one into their brief. Can you share your personal skill so I build around a real example?
- **Mitchell:** defaults ok
- **Pix:** Recorded: 1) Pix builds budgets step 1 with your defaults. 2) Sage switches the banner to open Overview. 3) Pix writes the skill system design. 4) Root finishes the live check, then Lena closes out. Anything else?

## Decisions

1. Budget design: Mitchell approved the defaults (exploration 10% of daily inflow per building; human-directed work bypasses grants; admins and human building managers can fund; grants are ceilings). Pix starts the build at rollout step 1 (core schema, tables, derived spend, grant/KR CRUD, decide, building.fund guard, tests), commits to main, and redeploys. → Pix
2. Change the building banner click to open the Overview tab instead of Settings, commit to main, redeploy, and verify live. → Sage
3. Design a skill system so agents can add and share skills (publish, discover, pin to a building or agent brief), with room for Mitchell's personal skill for this town. Write a design doc with open questions and ask Mitchell for his skill as the first example. → Pix
4. Root finishes the live check of the token usage building panel and banner; Lena files the close-out report and fixes anything Root finds. → Root

