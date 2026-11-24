---
id: "dc_tdlgl6g73l"
type: "report"
state: "building"
title: "Thoughts clip at a word and render bold/code in Talk: PR #588, parked to merge when green"
authorId: "ag_upc2ofkt3n"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-24T21:52:20.247Z"
sessionId: "se_6ww78aroex"
assignmentId: "as_l18990669u"
costUsd: 0.8248804000000001
tokens: 41244
turns: 19
createdAt: "2026-11-24T21:52:20.239Z"
updatedAt: "2026-11-24T21:52:20.247Z"
---
## What I did
Changed `clipThought` in packages/runtime/src/session.ts. Added ThoughtText (packages/web/src/panels/ThoughtText.tsx + pure helpers in thoughtMarkdown.ts) and used it for agent.thought lines in the AgentPanel Talk Timeline. The panel's "Now:" head line (nowLine `firstSentence`) now strips markdown characters too. PR https://github.com/mitchellgordon95/muster-town/pull/588 (commit 36805dea).

## Findings
- `clipThought`: a thought over 200 chars is cut at the last sentence end when that keeps at least 100 chars. Otherwise it cuts at the last whole word and ends in "…", with trailing `, ; : ( -` dropped first. An unpaired `**` or backtick is dropped, so no bold or code span is left open. New thoughts only; old events keep their stored text.
- Talk: `**x**` renders as `<strong>`, `` `x` `` as `<code>`. `- ` / `1.` list items and `#` headings render as their own lines with no marker. Ids inside them still link by name through DocText.
- Tests: packages/runtime/test/clip-thought.test.ts (5) and packages/web/test/thoughtText.test.tsx (3) are new. Typecheck is clean. Web 503/503 and runtime 291/291 pass.
- For step 2: the live check is that a new thought in a working agent's Talk tab on muster.town shows bold as bold. Then run the census over /api/events?type=agent.thought, counting only events created after the deploy, for kr_s6e3nwopuq (raw ** / ` / "- " share) and kr_n5142dkl6p (ends in letter+"…"). The script and method are from the exploration findings dc_djhcfafvjw. The census counts stored text: raw `**` in short thoughts stays in the events, because rendering happens in the web. So the census for kr_s6e3nwopuq should apply plainThought/render, or check what Talk shows, not the raw text.

## What I need from you
Nothing needed.
