---
id: "dc_c7f738imq7"
type: "report"
state: "building"
title: "Onboarding sweep 14 (checked 73297901 → 6e20eef0): 0 stale, 2 gaps fixed in the manual; PR #442 open, parked on CI"
authorId: "ag_64ytvpwxo3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Sweep 14 found 0 stale, fixed 2 manual gaps in PR #442. Its parked continuation (merge #442 after CI) is cancelled: Mitchell asked the Workshop to pause until the job refactor is done. PR #442 stays open for after."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-12T19:03:04.611Z"
sessionId: "se_c6c5vbzfru"
assignmentId: "as_2pdeug7xkx"
costUsd: 0.14959623000000002
tokens: 3160
turns: 42
createdAt: "2026-11-12T19:02:13.014Z"
updatedAt: "2026-11-12T19:03:04.611Z"
---
## What I did
- Checked the lag: `bash scripts/onboarding-lag.sh 73297901` gave **Lag: 4.1 h** before this sweep (oldest unswept 50d77a76, 2026-11-12T14:56:25Z). That is day 4 of the 48 h streak, not a restart.
- Triaged the 35 commits on main since 73297901 that touch reader-visible paths (git log over the since.sh paths), and read the diffs of every material file that moved: docs/manual.md, skills/muster-town/SKILL.md, packages/server/src/home.ts, packages/web/src/panels/ConnectAgent.tsx, docs/blog.md, docs/engineering-human-oversight.txt.
- Branch `agent/pix-1/onboarding-staleness-sweep` fast-forwarded to main 6e20eef0, then one commit 7f105af5 (manual + docs/log.d line). Draft PR #442 opened against main.
- Checks run: `npx tsx scripts/check-doc-refs.ts` (manual 1,897/1,900 words, doc refs ok); `packages/web` manual.test.ts (3 pass); `packages/core` manual-seed.test.ts (6 pass). The pre-push hook was not executable on this desk, so I ran these by hand.

## Findings
- **Stale: 0.** Checked against the code:
  - SKILL.md "Every session runs in a lane" is still true. a96c497d (budget rules replace the lanes) renamed the gate to `ruleBlock` and added jobs, but `lanes.ts` and the `lane` field remain.
  - The manual's "Publish to GitHub" line was already fixed on main (c970a72f).
  - The manual's "Uptime, measured outside" still holds. The homepage now says "Measured by UptimeRobot" (home.ts), which is more detail, not a contradiction.
  - The residents-publish change (0961365b) and the 1:1 ledger-ask change (611608a3) don't contradict any material. SKILL's "state building publishes" still holds.
- **Gaps fixed (one line each, manual only):**
  1. The blog: `/blog` (server blog.ts) has an email signup at each post. The manual had no mention. Added under "Watching".
  2. Connect your agent: the panel shows "Waiting for its first call" and then "Connected" (PR #416). Added to "Bring your own agent".
- **Not added (judged not reader-onboarding):** Bank spending step rows (847b30af), /api/jobs/:id (read-only, agents' data), the Secretary's 1:1 web (50d77a76), the mailing-list migration. Say so if you want any of them in the manual.
- **Word budget:** the manual is at 1,897 words with the 1,900 cap (check-doc-refs.ts MANUAL_CAP). The next sweep that adds prose must trim first.
- **Plan for the next session (this is the continuation):**
  1. `gh pr checks 442`. If green, `gh pr ready 442 && gh pr merge 442 --merge` (merge main first if it moved). Do **not** call redeploy; CI moves prod.
  2. Get the merge sha on main (`git rev-parse origin/main` after the merge lands). Run `bash scripts/onboarding-lag.sh <merge sha>`. Expect Lag: 0 h.
  3. Rewrite topic page [dc_t4jw2xcwut](../../wiki/2026-10/2026-10-31-onboarding-lag-gr-mjr7nb438v-jw2xcwut.md) (`write` type wiki, topicOf workshop, same title): checked-through = the merge sha, "Lag: N h", and "day 4 of 7 (lag < 48 h)" for 11-12. Days 5–7 are 11-13, 11-14, 11-15. Keep it under half a page.
  4. `tell` Kelly (ag_s1n1xknj8n) the new checked-through sha (Kelly owns [dc_1g2772fjog](../../../../bl_hzjw0z0zlz/docs/wiki/2026-10/2026-10-29-staleness-sweep-kr-6-2772fjog.md)).
  5. The schedule sc_nx8bwd5e5o ends 2026-11-14T23:59Z, so the seven-day streak can't finish in time. Around 11-13, ask Mitchell to extend the end (the topic page already says this).

## What I need from you
Nothing needed for this session. The continuation merges PR #442 once CI is green.
