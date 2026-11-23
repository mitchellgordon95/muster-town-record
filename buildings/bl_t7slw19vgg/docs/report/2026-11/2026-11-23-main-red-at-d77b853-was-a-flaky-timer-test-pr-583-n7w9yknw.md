---
id: "dc_tkn7w9yknw"
type: "report"
state: "building"
title: "Main red at d77b853 was a flaky timer test: PR #583 sets the cap to 250 ms, parked to merge when green"
authorId: "ag_a8e8xc8m0u"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:49:36.210Z"
sessionId: "se_enub6tz6pd"
assignmentId: "as_34tt2c8kwl"
costUsd: 0.45008790000000004
tokens: 22504
turns: 6
createdAt: "2026-11-23T16:49:36.204Z"
updatedAt: "2026-11-23T16:49:36.210Z"
---
## What I did
I read main run 45219693650. It failed on one test only: packages/core test/export-import.test.ts, "off the main thread: a 5 ms timer never gaps 100 ms while a large town exports". The gap was 102 ms against a 100 ms cap. The test passed 3 times out of 3 on my desk, where the export takes about 1.7 s. Mara's note says it also failed on PR runs 45057517303, 44554463592 and 44014758835, all on vitest 3. So #575 and vitest 5 did not cause it. I followed her narrow fix and opened PR https://github.com/mitchellgordon95/muster-town/pull/583.

## Findings
- **The change is one test.** The cap goes from 100 ms to 250 ms, with a comment that cites the run. The `took > 100` guard is unchanged.
- **The test still catches a blocked loop.** A blocked main thread gaps for about the whole export, over 1 s.
- **Checks pass on my desk.** All 9 tests in export-import pass, and so does the typecheck.
- **Main was not green yet when I checked.** The runs on e3fd899 (45220276491) and 172c4ab were still going. Whichever way they end, #583 removes the flake.
- **The fixing commit** is the squash of #583, once it merges.

## What I need from you
Nothing needed.
