---
id: "dc_40adieq14q"
type: "report"
state: "building"
title: "PR #579: weekly audit fails on dev advisories too; throwaway #580 proved it; parked merge-when-green"
authorId: "ag_wac46xtbbb"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:45:18.050Z"
sessionId: "se_cxcb4dukny"
assignmentId: "as_twg5nstguy"
costUsd: 0.5657231
tokens: 28286
turns: 15
createdAt: "2026-11-23T16:45:17.964Z"
updatedAt: "2026-11-23T16:45:18.050Z"
---
## What I did
I added a second step to `.github/workflows/audit.yml`: `npm audit --audit-level=high` over all dependencies, dev included. The prod step is unchanged, and the new step has `if: !cancelled()` so it runs even when the prod step fails. I updated the audit line in AGENTS.md step 6 and added a docs/log.d entry. This is PR #579 (https://github.com/mitchellgordon95/muster-town/pull/579), and it does not touch ci.yml. I opened throwaway PR #580, read its audit run and closed it unmerged. I rewrote the topic page Dependency advisories ([dc_o70qzef90k](../../wiki/2026-10/2026-10-31-dependency-advisories-0qzef90k.md)). PR #579 is parked to merge when green.

## Findings
- **The proof worked.** #580 pinned happy-dom 20.14.6 on top of #579, and its audit run 45219802785 shows:
  - "audit production dependencies": success
  - "audit all dependencies, dev included": failure, naming `happy-dom <=21.0.3, Severity: high` (GHSA-834v-8h66-3h79 and GHSA-c8p4-j97h-3vg8)
  - #580 is closed unmerged and its branch is deleted.
- **kr_lme35mttqy (claimable):** #574 is on main as ea638493, and `npm audit` on that tree prints "found 0 vulnerabilities".
- **kr_h37fmyne4l (claimable once #579 merges):** audit.yml has the all-deps step, the throwaway PR failed and named the advisory, and ci.yml is unchanged.
- **kr_ky260b3xlu (not yet measurable):**
  - Early sign: #574's own CI check (run 45218333594) ran tests in 106 s on vitest 5. The last vitest 3 main run (45218575281) took 92 s. The cap is 126 s.
  - The KR counts the first 5 green main push runs after ea638493. None had finished when I checked, because each push to main cancels the running check.
  - The close should wait for those 5 runs, or for a scheduled read on about 2026-11-25.
- **Gotcha:** audit.yml's path filter does not include audit.yml itself. #579 alone triggers no audit run, so the proof needed a lock change.

## What I need from you
Nothing needed.
