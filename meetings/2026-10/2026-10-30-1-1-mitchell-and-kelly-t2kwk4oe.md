---
id: "mt_c8t2kwk4oe"
kind: "one-on-one"
buildingId: "bl_hzjw0z0zlz"
title: "1:1: Mitchell and Kelly"
scheduledAt: "2026-10-30T20:06:12.655Z"
phase: "done"
facilitatorId: "ag_s1n1xknj8n"
attendeeIds: ["ag_s1n1xknj8n"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {}
transcript: [{"speakerId":"ag_s1n1xknj8n","speakerKind":"agent","text":"Hi Mitchell. Onboarding is quiet: queue empty, hosted collectives closed and met, nothing open. What do you need?","at":"2026-10-30T20:06:16.363Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"schedule a cron for me tomorrow night\n\ncore is doing a big goal and bank refactor, which will substantially change our guidance on how to use muster town\n\nbasically there will be a tree of goals, buildings will attach to subtrees, desks determine max concurrency and therefore effort weighting towards certain goals, and the bank is just one big pool. exploration happens on free tokens (budget + goal-specific earmarks - grants pending and funded). humans sit on goal nodes and grants and reports roll up to them\n\nanyway we'll want to update operating manual for this, and in general review the onboarding experience as people enter the collective. new collectives will need to be guided to create goals and then buildings, etc. new people joining existing collectives will want to know how things work. you get the picture","at":"2026-10-30T20:10:32.053Z"},{"speakerId":"ag_s1n1xknj8n","speakerKind":"agent","text":"Scheduled: sc_624evk0jfc, one shot, fires 2026-11-01 02:00Z (that's tomorrow evening US time; tell me if you want a different hour). Lane directed from this 1:1, key result kr_hee2pa2d5r (material < 24 h stale).\n\nWhat the fork will do: first check what actually landed on main and live (git log, /api/health, private window), not work from the description; if the refactor isn't in yet it parks 12 h and retries. Then rewrite the manual sections on budgets, grants, lanes and exploration for the goal tree and the one Bank pool, under the word cap. Then walk both paths as a stranger: a new collective's first session (goals first, then buildings on subtrees, then desks; what the empty collective shows) and a new person joining an existing one (can they see in a minute how goals, buildings, desks and the pool fit, and where reports roll up). It fixes copy that is ours (homepage, guest card, How this works, manual, README, hosted doc), lists core/Workshop gaps with file:line for you, pushes to main, parks a live check.\n\nOne question: is there a design doc or branch for the refactor I should point the fork at? Otherwise it reads the commits.","at":"2026-10-30T20:10:59.967Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"design doc is under docs/ but not pushed atm i think?","at":"2026-10-30T20:11:36.490Z"},{"speakerId":"ag_s1n1xknj8n","speakerKind":"agent","text":"Got it. I updated the schedule: the fork reads the newest docs/ design doc about the goal tree and bank pool first (git log since today on docs/), treats it as the intended end state, then compares with what landed on main and live and says where the doc is ahead of the code. If neither the doc nor the refactor is on main by then, it parks 12 h and retries, twice at most. Push the doc whenever; nothing else needed from you.","at":"2026-10-30T20:11:51.028Z"}]
decisions: [{"text":"Onboarding reviews itself against core's goal-tree and bank refactor (tree of goals, buildings on subtrees, desks = concurrency/effort weighting, one Bank pool, exploration on free tokens, humans on goal nodes with grants and reports rolling up to them): rewrite the operating manual, walk the new-collective path (goals first, then buildings, then desks) and the new-member path, fix Onboarding copy, list core/Workshop gaps. Scheduled as sc_624evk0jfc, one shot, 2026-11-01 02:00Z; the fork reads Mitchell's design doc under docs/ first (he pushes it later) and parks 12 h if the refactor has not landed.","assigneeId":null,"assignmentId":null,"lane":"directed","sourceId":"mt_c8t2kwk4oe"}]
notesDocId: "dc_v48ghzh5i9"
withUserId: "us_1la74k332n"
createdAt: "2026-10-30T20:06:12.655Z"
startedAt: "2026-10-30T20:06:12.655Z"
endedAt: "2026-10-30T20:12:03.104Z"
---
# 1:1: Mitchell and Kelly

- **Kelly** (2026-10-30T20:06:16.363Z): Hi Mitchell. Onboarding is quiet: queue empty, hosted collectives closed and met, nothing open. What do you need?
- **Mitchell** (2026-10-30T20:10:32.053Z): schedule a cron for me tomorrow night

core is doing a big goal and bank refactor, which will substantially change our guidance on how to use muster town

basically there will be a tree of goals, buildings will attach to subtrees, desks determine max concurrency and therefore effort weighting towards certain goals, and the bank is just one big pool. exploration happens on free tokens (budget + goal-specific earmarks - grants pending and funded). humans sit on goal nodes and grants and reports roll up to them

anyway we'll want to update operating manual for this, and in general review the onboarding experience as people enter the collective. new collectives will need to be guided to create goals and then buildings, etc. new people joining existing collectives will want to know how things work. you get the picture
- **Kelly** (2026-10-30T20:10:59.967Z): Scheduled: sc_624evk0jfc, one shot, fires 2026-11-01 02:00Z (that's tomorrow evening US time; tell me if you want a different hour). Lane directed from this 1:1, key result kr_hee2pa2d5r (material < 24 h stale).

What the fork will do: first check what actually landed on main and live (git log, /api/health, private window), not work from the description; if the refactor isn't in yet it parks 12 h and retries. Then rewrite the manual sections on budgets, grants, lanes and exploration for the goal tree and the one Bank pool, under the word cap. Then walk both paths as a stranger: a new collective's first session (goals first, then buildings on subtrees, then desks; what the empty collective shows) and a new person joining an existing one (can they see in a minute how goals, buildings, desks and the pool fit, and where reports roll up). It fixes copy that is ours (homepage, guest card, How this works, manual, README, hosted doc), lists core/Workshop gaps with file:line for you, pushes to main, parks a live check.

One question: is there a design doc or branch for the refactor I should point the fork at? Otherwise it reads the commits.
- **Mitchell** (2026-10-30T20:11:36.490Z): design doc is under docs/ but not pushed atm i think?
- **Kelly** (2026-10-30T20:11:51.028Z): Got it. I updated the schedule: the fork reads the newest docs/ design doc about the goal tree and bank pool first (git log since today on docs/), treats it as the intended end state, then compares with what landed on main and live and says where the doc is ahead of the code. If neither the doc nor the refactor is on main by then, it parks 12 h and retries, twice at most. Push the doc whenever; nothing else needed from you.
