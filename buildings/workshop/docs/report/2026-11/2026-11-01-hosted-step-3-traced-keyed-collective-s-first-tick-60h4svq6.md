---
id: "dc_uu60h4svq6"
type: "report"
state: "building"
title: "Hosted step 3 traced: keyed collective's first tick explores, proposal reaches founder, billed on their key (PR #252, test-only)"
authorId: "ag_tk1k9luced"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 3 traced in test (PR #252, CI green). Its merge continuation as_km3xgpu8j1 is held at the grant's checkpoint; the checkpoint rollup asks Mitchell to continue or cut."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T02:20:56.467Z"
sessionId: "se_rk0qr085sr"
assignmentId: "as_rg0txkvx7t"
costUsd: 2.628014199999999
tokens: 131401
turns: 52
createdAt: "2026-11-01T21:31:26.239Z"
updatedAt: "2026-11-02T02:20:56.467Z"
---
## What I did
Read hub.ts, core explore.ts / free-tokens.ts and the runtime's hosted path. Wrote a server test that runs `Hub.create` with a key, starts the hosted runtime the way main.ts does (fake SDK), and runs one tick. Then I opened PR #252 (https://github.com/mitchellgordon95/muster-town/pull/252, head aa0e662, main merged in) and rewrote the topic page [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md).

## Findings
- **Nothing was broken, so the PR adds a test and docs but no code change.** packages/server/test/hub-explore.test.ts has two cases, both green. The full server suite passes locally (259/259) and typecheck is green.
  1. **Started with a key:** the tick reserves one 100,000-token chunk under the founder's root. The Start credit is 1,000,000 and the operating reserve is 500,000, which leaves 500,000 free. The Workshop's manager-resident then runs in-process (hosted forces HostBackend). Its session shows `funding: api-key` and `credentialInputId` set to the founder's key input. The env carries the key and no OAuth token, and the Bank balance drops. Its `propose_grant` lands as "proposed", and `goalTree.route` sends it to the founder.
  2. **Started without a key (Hollyville's path):** the tick does nothing. Once a key is added at the Bank, the next tick reserves the chunk and a proposal lands.
- **Caveat:** a key credit of 600,000 tokens or less leaves less than one chunk free, so nothing explores. The Queue tab gives the reason. The Bank form defaults to 1M, so this only bites if a founder lowers it. docs/hosted-collectives.md now says so.
- **Not live-checked:** Hollyville has no key, and a guest can't start a keyed collective.
- **Rollup 37 item 14:** I couldn't add it to [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) ("You can only update documents you wrote"), so the manager needs to paste it:
  > 14. A hosted collective with a key explores on its first tick and its grant proposal reaches the founder (gr_5ltmbf3a2f step 3, kr_f722z9ut50; PR #252, test-only; page [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md)) · TRACED IN TEST, not live-checked · **What it is:** a stranger who starts a collective with a key gets work and a first grant proposal with no one in the Workshop doing anything. **What you'd see:** one grant proposal from its Workshop in that collective's Town Hall in-tray (Mine), a few minutes after Start. **Your call:** from a test GitHub account (or your own), start a throwaway collective on the muster.town homepage with a Console API key you're willing to spend about $2–5 on. Leave the 1M-token default. Within about 5–10 min its Town Hall in-tray should show one grant proposal and its Bank one session on your key. Then retire it in Planning → System → This collective. kr_f722z9ut50 is claimable once you see that.
- **Next session:** when PR #252's CI finishes, merge it if green and queue a redeploy. A test-only change needs no live check of its own.

## What I need from you
Nothing needed (the manager pastes item 14 above into [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md)).
