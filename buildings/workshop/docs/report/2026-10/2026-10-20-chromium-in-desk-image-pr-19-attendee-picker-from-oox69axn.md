---
id: "dc_cuoox69axn"
type: "report"
state: "building"
title: "Chromium in desk image (PR #19); attendee picker from #18 checked in a browser and works"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "do it"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:49:37.468Z"
sessionId: "se_y9ae0phm9y"
assignmentId: "as_irnu47e7lm"
costUsd: 0.5134692000000001
tokens: 30825
turns: 29
createdAt: "2026-10-20T03:44:38.180Z"
updatedAt: "2026-10-20T03:49:37.468Z"
---
## What I did
- My last session already opened draft PR #19 (https://github.com/mitchellgordon95/agent-town/pull/19). It adds Debian `chromium` and fonts to `packages/desk/Dockerfile` and sets `CHROME_PATH`/`PUPPETEER_EXECUTABLE_PATH`. The `chromium` package also brings in libnspr4, libnss3, libgbm1 and the other shared libraries headless Chromium needs. This session I left it as it was.
- My desk still runs the old container and I have no root, so I couldn't install packages. Instead I downloaded the missing Debian bookworm libraries (13 sonames, arm64) into `~/aptroot` without root and pointed `LD_LIBRARY_PATH` at them. With that, Playwright's chrome-headless-shell (build 1248) runs.
- Ran PR #18's web UI with `VITE_MOCK=1` and drove it with playwright-core. Posted the results on #18: https://github.com/mitchellgordon95/agent-town/pull/18#issuecomment-6282831692

## Findings
- **The #18 picker works in a lab.** On Carbon Cycle Lab → Meetings it shows "Invite: 6 picked". The 6 residents are checked and the 3 people from other buildings are not. I unchecked Ingrid, checked Wren, then clicked Call meeting. The new meeting's attendees were exactly Mei, Moss, Noor, Ravi, Tomas and Wren.
- **It works in Town Hall.** It shows "Invite: default (managers, reviewers and moderators)" with all 9 agents unchecked.
- No page errors or console errors.
- **Not checked separately:** the meeting room's "Call a standup" button (`MeetingPanel` → `CallMeeting`). It uses the same hook and component.
- **Existing desks won't get Chromium until they're recreated.** Even after #19 merges, they keep their old container. Someone has to run `npm run desk:build` and then `docker rm -f` each desk container (the home volume is kept).

## What I need from you
Merge PR #19 and #18, then rebuild the desk image (`npm run desk:build`) and recreate the desk containers.

## Reply from Mitchell (2026-10-19 23:49)

do it

