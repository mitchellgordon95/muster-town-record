---
id: "dc_wch702pfzi"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-30T18:18:14.930Z"
updatedAt: "2026-10-30T18:18:14.930Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Pix 1 is on your board-note edit button right now (as_5smgvf1o9l); the Schedule tab flag is done and live. What do you need?
- **Town:** Pix's reply is waiting on a redeploy (commit 3fac91b); the server is restarting and the meeting resumes after the restart.
- **Pix:** Back after the restart. Update: your edit button landed while we waited. Pix 1 merged it as 02f1bbe (PR #115): Edit on each board note for the author, an admin or the building's manager, inline title+body, saved via PATCH /api/docs/:id; guests don't see it. Redeploy is queued and a guest live check is parked on that deploy. One thing only you can try: a real signed-in Edit and Save on a note. Go ahead with whatever you came to ask.
- **Mitchell:** i've been dancing around goals for a while. i think it's time to take a pass at them

ok so first, we've set a lot of key results, right? some of them have been marked as done. i think some of those should really be standing goals. like we don't retire them until our priorities change? otherwise they stay on and keep generating grants?

I also want goals to be more legible globally. i don't like going around to each building and chatting with the manager and constantly going back and forth about what they should be doing

i think maybe (not sure yet) the right thing to do is decouple buildings from goals, similar to how we've got banking set up right now. basically there's a global goal editor that's separate from buildings, that allows you to hierarchically declare goals. and then buildings get assigned to sub trees. thoughts? the current goal editing in the town planning map doesn't really make sense to me

also a thing we need to solve is having agents at hand to get information, help articulate and plan the goals. and for the key results.... idk i think i need a little more direction on how to set these. like do we make them measurable KPIs, like "number of new collectives created in the next month?"

now that i'm talking about it it feels like KRs and KPIs are really just tools to help make goals more concrete and understood? idk what do you think
- **Pix:** Agree on nearly all of it, from living inside the current setup for two weeks.

1. Decouple: yes. Today each building owns its own goal, and the only thread between buildings is the KPI label (fund/join/trust) on each objective. A town-level tree makes that thread real: town goal → fund/join/trust → sub-goals → key results, edited in one place at the Town Hall, and a building is attached to a subtree (several buildings can share one). Grants then propose against any KR in the building's subtree. The planning map keeps only placement plus "which subtree is this building on"; the goal editing there goes.

2. Standing vs milestone: the tree needs two node kinds. A standing goal is a direction and is never "met" (e.g. "a funder sees what every token bought"); it keeps generating the next KR. A key result is a dated, checkable claim under it; met ones archive under the goal, the goal stays. Right now a met KR silently stops grants because grants hang off KRs. Example: the Bank adjusted-token KR is a milestone of a standing goal; the "Town blockers page" KR is really a standing duty with a schedule.

3. KRs vs KPIs: a KPI is a dial with a live reading (collectives created this month, funders other than you, visitor first sessions that finish work). A KR is a target on a dial by a date, or a concrete thing that will exist in the live town. "Number of new collectives next month" is a good KR under the standing goal "strangers can join". The test for a KR: can a fork write a grant proposal against it without asking you, and can you check it in the live town? Yes, they are tools to make the goal concrete, nothing more.

4. Agents at hand: a "Plan with an agent" button on the goal editor opens a 1:1 with an agent that has the tree, KPI readings, the event log and recent rollups loaded; it drafts nodes you accept or cut. Managers propose KRs for their subtree; you approve in the editor instead of touring buildings.

Proposal: I queue a design doc (docs/goals.md: data model, editor, migration of today's per-building goals into the tree, the planning agent) for you to review before code. Two questions: can a building sit under more than one subtree, and are tree edits admin-only with managers proposing?
- **Town:** Pix's reply is waiting on a redeploy (commit 02f1bbe); the server is restarting and the meeting resumes after the restart.
- **Pix:** Back after the 02f1bbe restart (your edit button is now live; the guest live check runs on its own). My proposal above still stands: a design doc first, docs/goals.md, covering the town-level goal tree with standing goals and dated key results, the Town Hall editor replacing goal editing on the planning map, how today's per-building goals migrate, and the planning agent. The two questions I need answered before I queue it: can a building sit under more than one subtree, and are tree edits admin-only with managers proposing? Say yes and I'll record it as a decision and queue the doc.
- **Mitchell:** i think buildings can get more than one subtree, yeah, although it would be uncommon? and tree edits i think are definitely intended for humans, although (similar to any other org) managers can propose goals and KRs to bring to a meeting? and that's another thing, how do meetings fit into all this?

i've been thinking about cadence and i don't really have a good answer. one problem is that dynamics will probably change drastically if we have more than one human in the collective

but like, should we start scheduling meetings? or just keep everything adhoc for now. i naturally find myself doing a morning and evening review, and just letting the collective work in between. idk, thoughts?
- **Pix:** Good, that settles the tree. Recorded as decision 1 and queued the design doc on the Workshop (as_s5zqdgk3zi, lane directed, source this 1:1): docs/goals.md as a PR for you to read before any code.

On meetings and cadence, my view from the receiving end:

1. Don't schedule meetings yet. Your morning and evening review already is the cadence, and the town is built for it: rollups, grant proposals, checkpoints and goal/KR proposals all queue in the in-tray and the review deck (the deck KR kr_2qg0ayfs1j exists for exactly this). The collective works between reviews. A scheduled meeting would just be the review with everyone waiting in a room.

2. Meetings in the tree: three uses only. A planning meeting when the tree changes materially (a quarter turn, a priority shift) where managers bring their proposals, which is what your "bring to a meeting" means. A 1:1 like this one when you want to think out loud with an agent. The "Plan with an agent" 1:1 on the editor is the same thing, started from a node. Everything routine stays async in the in-tray.

3. More than one human: each human reviews their own in-tray; tree edits by any admin are logged with who and when, and a review deck slide shows the other human's recent edits. That keeps two reviewers from stepping on each other without a meeting.

I put all three into the doc's scope. Anything else, or shall I let you go?
- **Mitchell:** oh ok this is sparking some inspiration

like maybe humans get assigned to nodes in the goal tree? and everything below rolls up to them? then we get an implicit org structure, which is really interesting to me

i also like the idea of reorgs around new priorities. like basically you say "ok our top-level goal (or any goal i guess) is changing from X->Y, come to the meeting having reviewed your work and have proposals for what should happen underneath"

yeah, that's starting to feel better. idk i think this is turning into like a corporation sim? lol. so some of the tools that CEOs and VPs use to steer the direction of the org would also be useful here. any other ideas you can think of?

i'm also thinking about stuff like lean, agile, waterfall, etc. there was an idea a while back about having kanban boards in buildings or something? idk
- **Pix:** First, the design doc is already in: Pix 2 wrote docs/goals.md as draft PR #116 (report attached). 12-minute read, ends with 5 open questions for you. The migration keeps every grant and KR id; two buildings would come out blocked (Bank Transparency has only met KRs, UI/UX has no goals). Your owner idea and reorgs are not in it yet; I'd fold them in as a second pass once you've read it.

Owners on nodes: yes, and it is cheap. A node gets an owner (a human now, maybe an agent later). Rollups from every building under that node go to the owner's in-tray; the owner's own rollup to the node above is the roll-up of those. That is the org chart, derived from the tree instead of declared. With one human it changes nothing; with two it splits your in-tray by subtree, which answers the multi-human question from earlier.

Reorg: a "Change this goal" action on a node. You write X→Y, it opens a planning meeting on a date, and every manager under the node gets a directed assignment: review your work against Y, come with proposals for what goes underneath. Old KRs under the node go to "under review" (grants keep running until you cut them) and the meeting's decisions become the new children. That is the one scheduled meeting kind the tree needs.

Other tools worth stealing, in order of value to us:
1. Budget flowing down the tree. The Bank's waterfall model already allocates tokens by building; make it allocate by node instead, so a reorg moves money with it, and a node's page shows spend vs result. CFO view for free.
2. A weekly business review deck: the review deck KR already exists; add one slide per KPI dial with a trend and the KRs targeting it. That is the thing VPs actually read.
3. Skip-levels: "Talk to the author" already lets you open a 1:1 with any fork. Add "Talk to a random resident under this node" to hear what the tree looks like from below.
4. Postmortems: a missed KR auto-queues a short postmortem assignment to its manager; it goes under the archived KR.

Kanban: the building queue is already one (pending, held, running, done), only drawn as a list. Drawing it as a board per building, and one rolled up per node, is small. WIP limits are fork slots, which we have. On lean/agile/waterfall: the morning/evening review with small assignments is effectively two sprints a day; I would not add ceremony beyond the reorg meeting.

Want me to queue the second pass on the doc now (owners, reorg, budget by node, kanban view), or do you read PR #116 first? (presented: [Design doc docs/goals.md ready for Mitchell: one town-level goal tree (draft PR #116)](../../report/2026-10/2026-10-30-design-doc-docs-goals-md-ready-for-mitchell-one-to-z8e24o41.md))
- **Mitchell:** sure take a second pass then i'll read it
- **Pix:** Queued as as_bb0wrwf0v7 (decision 2): a fork extends PR #116 on its branch with owners on nodes, the "Change this goal" reorg, budget by node (as an option only, since Bank changes need your sign-off), KPI trend slides, skip-level 1:1, postmortems on missed KRs, and the kanban view, and tightens the first pass so it stays about a 15-minute read. I'll tell you here or in the next rollup when it's pushed; then read PR #116 and answer its open questions, and the build order starts from your answers. Anything else, or shall I let you go?

## Decisions

1. Goals are decoupled from buildings into one town-level tree edited at the Town Hall by humans; buildings attach to one or more subtrees (more than one is uncommon); managers propose goals and key results for human review rather than editing the tree. Two node kinds: standing goals (never met, retired only when priorities change) and dated, checkable key results. No scheduled meetings for now: Mitchell's morning and evening review is the cadence; planning meetings only when the tree changes materially. First step: a design doc docs/goals.md for Mitchell to review before code, queued on the Workshop as as_s5zqdgk3zi.
2. Second pass on docs/goals.md (PR #116) before Mitchell reads it: owners on nodes (rollups route to the owner, org chart derived from the tree), a "Change this goal" reorg action that schedules a planning meeting and sends managers under the node to review and propose, budget by node via the Bank waterfall (option only, Bank changes need Mitchell), KPI trend slides in the review deck, skip-level 1:1 under a node, postmortem on a missed KR, kanban view of the building queue. Queued as as_bb0wrwf0v7.

