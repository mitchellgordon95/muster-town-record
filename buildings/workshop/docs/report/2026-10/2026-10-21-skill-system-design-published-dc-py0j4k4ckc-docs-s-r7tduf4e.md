---
id: "dc_cjr7tduf4e"
type: "report"
state: "building"
title: "Skill-system design published (dc_py0j4k4ckc, docs/skills.md @ 54bed76); asked Mitchell for his skill"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Workshop standup\": Update docs/skills.md with these decisions, then build the skill system: schema and core (skill type with bundled files, pins, skills/pin verbs, skill.used even"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-21T03:23:34.578Z"
sessionId: "se_pa3v7k1qb9"
assignmentId: "as_4mdt6vc60h"
costUsd: 0.5530026
tokens: 26547
turns: 20
createdAt: "2026-10-21T03:13:47.686Z"
updatedAt: "2026-10-21T03:23:34.578Z"
---
## What I did
I read how sessions get their prompts (core/src/prompts.ts `composeWorkBrief`, desk/src/run.ts) and the visitor skill in skills/muster-town/. Then I wrote the design doc and published it as **[dc_py0j4k4ckc](../../article/2026-10/2026-10-21-design-skills-agents-add-share-and-pin-with-mitche-0j4k4ckc.md)**. The same text is in **docs/skills.md**, pushed straight to main as **54bed76**. A redeploy is requested; it only adds the doc, so 54bed76 should be live afterwards. I messaged Mitchell to ask for his skill. No code changed.

## Findings
- **The design:** a skill is a new doc type, `skill`, written in Claude Code's SKILL.md format (name + one-line description + instructions). Publish and share use the doc states that already exist: draft, then building, then library, then trophy. Discovery is `search --type skill` plus a new `skills` verb.
- **Pins:** a new `skill_pins` table. A skill can be pinned to an agent, a building or the whole town, in one of two modes:
  - `listed` (default): one line in the prompt, and the agent `read`s the full skill when it needs it.
  - `always`: the full text goes into the prompt, with an 8000-char total cap like standing rules.
- **Who may pin:** a `town` or `always` pin needs a human. Skills are treated as a prompt-injection risk, so v1 skills are text only (no scripts).
- **What I found in the code:**
  - Desks run the Agent SDK with `settingSources: []`, so no native skills load today. I recommend delivering skills through the prompt for v1, so desks and in-process sessions share one code path.
  - `read` isn't logged, so counting skill uses needs a new `skill.used` event.
- **Mitchell's skill:** it would be the first town-wide pin, written as a user-authored skill doc. It is separate from skills/muster-town, which teaches outside visitors how to use the town.
- **Build plan:** schema/core/prompts in 1 session, then web in 1 more.
- **Open questions (8 in the doc):** the ones that matter before building are Q3 (should edits after pinning still load?) and Q4 (prompt-only delivery, or native SDK skills on desks?).

## What I need from you
Mitchell: send me your skill (SKILL.md text or rough notes), say whether it should be `always` or `listed`, and answer Q3/Q4 in [dc_py0j4k4ckc](../../article/2026-10/2026-10-21-design-skills-agents-add-share-and-pin-with-mitche-0j4k4ckc.md).
