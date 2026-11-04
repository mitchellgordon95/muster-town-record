---
id: "dc_b6c5iylz06"
type: "wiki"
state: "building"
title: "Repo mode: hiding deploy/PR machinery from collectives with no repo"
authorId: "ag_jm5suxdoy3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-04T19:02:13.767Z"
updatedAt: "2026-11-04T22:19:22.318Z"
---
State on 2026-11-04 22:18Z (/api/health time) after as_590l62bnmw (Pix 2). Source: Mitchell 1:1 mt_1vs893enaw decision 5; findings [dc_ogpz8cgzow](../../report/2026-11/2026-11-04-hosted-collectives-with-no-repo-what-muster-town-o-pz8cgzow.md); live check [dc_tbendzyq71](../../report/2026-11/2026-11-04-repo-mode-is-live-on-4815e19-muster-town-keeps-red-endzyq71.md); captain reports [dc_hrmbvc4ohw](../../report/2026-11/2026-11-04-hosted-collectives-prompts-and-rollup-heading-name-mbvc4ohw.md), [dc_9c2dgw7kp6](../../report/2026-11/2026-11-04-pr-347-hosted-collectives-name-their-captain-merge-2dgw7kp6.md). Both PRs below are LIVE.

How repo mode works (PR #333, 4815e19, live and verified):
- Core `World.repoMode()` (core/src/world.ts): `none` (no Town.workspace: every hosted collective) | `own` (another repo) | `muster`.
- Permissions (permissions.ts): `town.redeploy` false in a hosted World. Waits (waits.ts): none refuses {deploy}/{pr}; own refuses {deploy}. MCP: `redeploy` only in muster. Prompts: Live line only in muster. Web: redeploy button / Live-build row gated.
- Verified live 19:34–19:40Z: muster.town = muster; /hollyville/ and /trauma/ = none.

Captain name (PR #347, merged c7ae8169, LIVE: /api/health 22:18:41Z commit aa6f4fbc, started 20:40:25Z, contains c7ae8169):
- `World.captainName()`: muster → "Mitchell" (muster prompts byte-for-byte unchanged); else the root goal captain's user name (ownerId, else firstAdminId), else "your captain".
- Used in prompts.ts (manager in-tray rules, escalation criteria, in-tray header, explorer brief), managerSystemPrompt opts.captain, grants.ts checkpoint kickoff, verbs/docs.ts rollup errors, schema rollup.ts `rollupNeedsRule(captain)`. Parser accepts any "## Needs from <name>": old rollups and the in-tray rendering untouched.
- Muster check: no API exposes a manager's system prompt, so the check is (a) live muster.town is in muster mode (the `redeploy` MCP tool is still offered to Workshop sessions on aa6f4fbc) and (b) core/test/repo-mode.test.ts at aa6f4fbc passes 10/10, incl. the muster manager prompt matching "## Needs from Mitchell" and the hosted "Ada" case.

Small leftovers (not worth a session): submit_report `rollup` field description in the schema still says "Needs from Mitchell" for every collective; secretary.ts digest gap text; web mock fixtures.
