---
id: "dc_nfoa7wzmu6"
type: "report"
state: "building"
title: "Pin design written (dc_8194l8soj4); grant gr_y4s2j99vgm proposed, 450k, three M steps"
authorId: "ag_00q3kig0qr"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Design dc_8194l8soj4 read: matches Mitchell's mapping (mt_uarrn0kco1 decision 1) and the pure-core rule. gr_y4s2j99vgm waits for a human in the Town Hall in-tray; its card is filed. The living-page re-proposal is folded into step 3 (Town Hall docs tagged town-page become town/listed pins; the Secretary writes them), so no separate re-proposal goes out unless Mitchell asks for one."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-16T18:47:51.264Z"
sessionId: "se_o63eg2pd46"
assignmentId: "as_vxs0h5frdi"
costUsd: 1.2186723
tokens: 60934
turns: 20
createdAt: "2026-11-16T18:47:12.316Z"
updatedAt: "2026-11-16T18:47:51.264Z"
---
## What I did
Read the five ways a doc gets into a session today: skills.ts (forAgent, skillsBlock, authorize), prompts.ts townRulesBlock and its callers, operating-manual.ts, secretary.ts policyLedgerBlock, dictionary.ts dictionaryBlock, memory.ts pagesForAssignment/forkMemoryBlock, verbs/social.ts:82, secrets.ts:207, migration 026. Wrote the design [dc_8194l8soj4](../../article/2026-11/2026-11-16-design-the-pin-one-abstraction-for-every-doc-that-94l8soj4.md) (article, in the cabinet). Proposed grant gr_y4s2j99vgm and started the topic page "Pins" [dc_8je9babk61](../../wiki/2026-11/2026-11-16-pins-e9babk61.md). Wrote no code.

## Findings
- **Design [dc_8194l8soj4](../../article/2026-11/2026-11-16-design-the-pin-one-abstraction-for-every-doc-that-94l8soj4.md).** A pin is {docId, scope, targetId, mode, pinnedBy, byHuman, seeded}. Migration 118 renames skill_pins to pins, renames skillId to docId and adds `seeded`. The pure core `pins.ts` (resolvePins, pinnedPagesBlock) builds one "## Pinned pages" block. Always-mode entries come first, ordered town → building → agent so the prompt cache prefix stays stable. They share one cap, proposed at 16,000 chars (today's two 8,000 caps added together). Entries past the cap are listed instead. Listed lines come after.
- **Seeding.** Mitchell's mapping is seeded when each doc is created (INSERT OR IGNORE), plus a one-time back-fill in the migration. Nothing is seeded at boot, so a human's unpin stays in place.
- **Write rights.** Who may write a doc stays a rule on the doc. The Secretary's owner line becomes a generic "you keep this page" line, driven by canWrite.
- **Deleted.** operatingManualBlock, MANUAL_PIN_CAP, policyLedgerBlock, dictionaryBlock, townRulesBlock, skillsBlock, and the fork's title-match page guess.
- **Kept.** Secrets granted through skill pins still reach whoever has the skill pinned (secrets.ts:207). An assignment's explicit `pages` stay, as always-mode entries for that session only.
- **Who may pin.** Today's skills rule, applied to any doc.
- **Grant gr_y4s2j99vgm** "One pin for every doc in a session" is proposed. The ask is 450,000 tokens (M+M+M). The estimate line says 3 similar grants spent 368k–698k.
  - Step 1: the pin table, the pure core with property tests, and skills moved onto pins.
  - Step 2: manual, ledger and dictionary become town pins.
  - Step 3: topic pages, the manager's wiki and town pages become pins.
  - KRs: kr_o377rj6f34, kr_npbre8uaef, kr_yewkqe5nmv. The card says Mitchell asked for this in mt_uarrn0kco1.
- **Unknowns (design §10).**
  - Under the mapping, forks would see the manager's wiki as a listed pin, not full text. Step 3 measures what that changes.
  - The 16,000-char cap is a guess; I have not measured it.
  - Town board FYIs are not in the mapping and stay as they are.
  - The pin table rename changes the schema but no data. The step 1 PR must say so.

## What I need from you
Fund, counter or reject gr_y4s2j99vgm in the Town Hall in-tray.
