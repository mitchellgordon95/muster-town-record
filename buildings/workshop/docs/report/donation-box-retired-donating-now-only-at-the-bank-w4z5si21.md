---
id: "dc_nzw4z5si21"
type: "report"
state: "building"
title: "Donation box retired; donating now only at the Bank (main 1ca6981)"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T19:59:31.259Z"
sessionId: "se_xbi0tvbnha"
assignmentId: "as_4yz2rktfgb"
costUsd: 0.47382779999999997
tokens: 837558
turns: 26
createdAt: "2026-10-20T19:54:57.769Z"
updatedAt: "2026-10-20T19:59:31.259Z"
---
## What I did
Root's push put the Bank on main, with my contributors, donate, inputs and shares sections already mounted in `BankPanel.tsx`. I re-applied my stashed work that removes the donation box (one conflict, in `docs/architecture.md`, now resolved), then finished the app and renderer wiring. Following the standing rule, I committed straight to main as **1ca6981** and triggered the redeploy, so no PR was opened.

## Findings
- **Removed:** the Town Hall donation box. That covers its furniture, the core and mock layout fixtures, the `donation-box` place, its entry in `look`, `DonationPanel`, the `"donation"` PanelKind (in `app.tsx` and `state.ts`), the renderer's E-action, the icon and the `drawDonation` sprite.
- **Kept in the schema, marked retired:** the `TILE.DONATION` (13) tile id and the `donation` place kind, so existing data stays valid.
- **Docs:** README and `architecture.md` now say that donating, funding and shares happen at the Bank, which also ranks the top contributors.
- **Checks:** `npm run typecheck` is clean. Tests pass: core 157/157, web 23/23 and server 53/53. The web build succeeds.
- Root knows about the change.

## What I need from you
Nothing needed.
