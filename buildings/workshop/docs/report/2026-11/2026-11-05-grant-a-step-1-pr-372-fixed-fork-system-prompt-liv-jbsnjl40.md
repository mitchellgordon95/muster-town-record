---
id: "dc_65jbsnjl40"
type: "report"
state: "building"
title: "Grant A step 1: PR #372 (fixed fork system prompt, live state in the first message); parked on its CI"
authorId: "ag_v3s41gey65"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 of grant A is a draft PR (#372) with the byte-identical-prompt test; its continuation as_kehi8j5eaj already waits on PR #372's CI (merge if green, park on the deploy, then the live cache check with the per-model fork hit share Mitchell asked for in mt_4ekr1gg27a). Nothing else to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T21:12:24.074Z"
sessionId: "se_dilhygbgi4"
assignmentId: "as_qug2qgx7pl"
costUsd: 2.3346448
tokens: 116732
turns: 10
createdAt: "2026-11-05T21:12:08.014Z"
updatedAt: "2026-11-05T21:12:24.074Z"
---
## What I did
I split a work session's prompt the way the team-lead prompt is already split. The system prompt now holds only what is the same every session, and everything live moves into the first message, right after the clock. I opened draft PR https://github.com/mitchellgordon95/muster-town/pull/372 (commit 147bad4f plus a test fix) and parked on its CI. I also rewrote the topic page [dc_p73nckwcta](../../wiki/2026-11/2026-11-05-grant-a-one-stable-fork-prompt-per-building-gr-9kt-3nckwcta.md) and replied to Pix about Mitchell's per-model note (ms_lkhfz1v5jr).

## Findings
- **System prompt** (`workSystemPrompt` + `fixedParts`):
  - A fork's prompt is byte-identical for every fork of its building. It opens "You are a fork of <manager>, the manager of the <building>" and carries no name, id, lane or goals-and-grants block, town board, memory or branch.
  - A fork's skills are its manager's pins (`forAgent(forkOf)`).
  - A manager's work session keeps its fixed in-tray rules in the system prompt.
  - The Code access block is generic and no longer names the branch.
- **First message** (`workStateBlock`), after the clock:
  - the fork's name and id;
  - the goals and grants, with this session's lane;
  - for a manager: in-tray rows, team and grants;
  - the town-wide FYIs;
  - the memory. A fork gets its manager's wiki excerpt, its topic pages and the log tail, with the caps unchanged. A manager gets the index of its wiki, and reads pages on demand as on team-lead wakes.
  - "## Your branch", with the push command.
- **Callers**: `composeWorkBrief` (desks) and the runtime's in-process `runWorkSession` both use the new layout. The desk's run.ts is unchanged, and so are grants.ts, the TTL and the Bank.
- **Test (kr_9jf2lzz98p)**: in prompts.test.ts, two forks of one building get a byte-identical `system` even though they have different assignments, pages, lanes and branches, and the clock, wiki, log, topic pages and town board change between them. The prompt starts with the clock, then the state. The same holds for two work sessions of one manager. I updated the six tests that asserted the old layout.
- **Local runs**:
  - typecheck green and core 793/793 on 147bad4f;
  - the runtime run failed 1 of 239 (work.test asserted the old layout); fixed in the follow-up commit, and work.test now passes 9/9. I did not re-run the whole runtime suite after the fix; CI covers it.
  - server desk.test 10/10. I did not run `npm run check`; CI covers it.
- **Live-check plan** (amended by Mitchell in 1:1 mt_4ekr1gg27a: the cache is per model, so the gain is fork to fork within one building on the same model):
  - after the deploy, report the share of fork first turns in the hour whose `cache_read_input_tokens` grew by about the system prompt's size;
  - report each fork's model and its turn-1 write (target under 8k raw, baseline 20.8k median, n=21).
  - If the second fork on the same model still writes the whole prefix, the grant's stop condition is met.
- The stop condition's other half (does the report still cite the manager's pages or the chain?) can only be checked on a report written under the new layout, after the deploy.

## What I need from you
Nothing needed.
