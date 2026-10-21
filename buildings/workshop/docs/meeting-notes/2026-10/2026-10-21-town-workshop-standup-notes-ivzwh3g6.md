---
id: "dc_6oivzwh3g6"
type: "meeting-notes"
state: "building"
title: "Town Workshop standup — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-21T03:23:30.365Z"
updatedAt: "2026-10-21T03:23:34.581Z"
---
# Town Workshop standup

Kind: standup. Facilitator: Pix. Attendees: Pix.

## Agenda

(none)

## Summaries

**Pix:** Did: I wrote and published the skill-system design, and asked Mitchell for his skill.
Next: Once Mitchell answers two open questions, I'll build the data and prompt side.
Need: Mitchell, please send your skill notes, say whether it's always or listed, and answer the two open questions.

## Discussion

- **Pix:** Agenda: 1) Skills design doc (docs/skills.md) is published. 2) Blocked on Mitchell: his skill notes, whether it's always-on or listed, and the two open questions in the doc. 3) Next step: build the data and prompt side once those are answered.
- **Mitchell:** let's chat about the skills. so skills are basically files in the file cabinet under a folder called skills? is that correct?

and then what are the questions you need me to answer
- **Pix:** Close. A skill is a doc of a new type, "skill", rather than a folder. It uses the SKILL.md format: a name, a one-line "when to use" description, then the instructions. A draft is private. Published to a building, it sits in that building's filing cabinet. Promoted to the library, the whole town can use it. A "pin" puts it into sessions, scoped to one agent, one building or the whole town. Each pin is either "listed" (only the name and description go into the prompt, and the agent reads the full skill when it needs it) or "always" (the full text goes into the prompt).
The two questions I need answered:
1) Edits after pinning: if someone edits a skill that's already pinned, should sessions get the new text right away, or should it stop loading until someone pins it again?
2) Delivery: should skills go in through our own prompt block (my recommendation: it works for desks and in-process sessions, and we can count uses), or should desks load them as native Claude Code skills?
Also: please send your skill text, or just notes, and say whether it should be always or listed.
- **Mitchell:** for (1) whatever's easier. i assume the former

for (2) sure we can do our own prompt injection that's fine. 

i do kind of think skills should be folders and have scripts bundled possibly

once you implement the system i'll have a claude code agent add the skill i want
- **Pix:** Got it: (1) edits load right away, (2) our own prompt block. I'll make skills folders: a SKILL.md plus bundled files (scripts, references), stored with the skill. A session sees the folder's file list and reads files on demand. On desks, the agent can unpack the folder and run the scripts. One guard: those scripts run with the agent's GitHub token, so pinning a skill that has scripts into anyone else's sessions will need a human. I'll update the design doc, build schema, core and prompts first, then the web side, and tell you when a Claude Code agent can add your skill.

## Decisions

(none)

## Decisions recorded after close
- Skills decisions from Mitchell: (1) when a pinned skill is edited, sessions get the new text right away (no freezing). (2) Delivery is our own prompt block via composeWorkBrief, not native SDK skills. (3) Skills are folders: a SKILL.md plus bundled files and scripts. Pinning a skill that has scripts into anyone else's sessions needs a human.
- Update docs/skills.md with these decisions, then build the skill system: schema and core (skill type with bundled files, pins, skills/pin verbs, skill.used event), the prompt skills block, then REST and web. Commit to main, redeploy, and tell Mitchell when a Claude Code agent can add his skill. (→ Pix)

