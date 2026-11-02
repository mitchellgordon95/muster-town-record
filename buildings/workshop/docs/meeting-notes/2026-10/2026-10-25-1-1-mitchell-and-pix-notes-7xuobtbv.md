---
id: "dc_bo7xuobtbv"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-25T16:52:51.092Z"
updatedAt: "2026-10-25T16:52:51.092Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix.

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. The re-proposal of gr_jqsqra0dlx at your one-day counter is in progress, and Lena is on the millions inputs. What do you need?
- **Mitchell:** Wait, so just to be clear, buildings have goals, and goals have KRs, right? and then a grant is an implementation plan for a KR with a budget?
- **Pix:** Close, but the KRs hang off the grant, not the goal. The chain as built: the town has a goal, each building has a goal under it (one sentence, no KRs of its own). A grant is a manager's proposal toward the building goal: an objective, 2–3 key results you can check in the live town, a token ask and a stop condition. You fund, counter or cut it. Assignments then run in a lane: "grant" names a funded grant plus one of its KRs; "exploration" names a goal gap and spends from the daily allowance (4M tokens/day here). So a grant is less "a plan for one KR" and more "a funded objective, with its KRs as the checkable promises". If you'd rather KRs live on the building goal and grants fund one KR each, that's a real change to the model, and we should decide it now before the re-proposal lands.
- **Mitchell:** yeah what i said is what it should be
- **Pix:** Got it, that's the model then. What changes: (1) KRs move onto the building goal, set by you in Building → Settings (the manager can propose them to you in a 1:1, but only a human writes them, same as the goal). (2) A grant names one KR: it carries the plan (objective, how, stop condition) and a token ask in millions; funding it runs that plan. (3) The grant lane just names the grant; exploration names a KR with no funded grant, or a gap. (4) Checkpoints and the board's KR view read KR status off the goal, not the grant. Two yes/no questions before I assign it: (a) The Workshop's three KRs from gr_jqsqra0dlx (works autonomously; one explicit blocker; fund/checkpoint/new-KR wakes the manager) become the Workshop goal's KRs. Yes? (b) I withdraw the countered grant and re-propose one grant per KR, starting with KR1 at ~13M tokens, rather than one grant for all three. Yes? Plan: Lena owns the model change (core, schema, migration, API), Root the UI (KRs on settings, grant form picks a KR, board), Keel the live check after deploy.
- **Pix:** One note: a redeploy is queued and waits for this 1:1 session to end before the server restarts, so the new build goes live once you close the meeting. Nothing in it changes the answers above. Your two yes/no answers and I'll assign.
- **Mitchell:** to be clear, a human writes goals with the assistance of a manager

yes the grant names a KR, and what was formerly KRs on the grant can still be listed as like a testing plan or something

no to a, we still need to discuss goals. that's why i was saying, if the building doesn't have any KRs to explore against or any grants to implement, it should clearly show as blocked and the manager should proactively try to fix the block by getting human decisions and input

for b, looks like everyone's already done with their work so just do whatever works atm
- **Mitchell:** hello?

## Decisions

(none)
