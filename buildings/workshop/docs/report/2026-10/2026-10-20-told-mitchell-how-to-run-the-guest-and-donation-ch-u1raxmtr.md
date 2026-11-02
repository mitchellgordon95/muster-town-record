---
id: "dc_vru1raxmtr"
type: "report"
state: "building"
title: "Told Mitchell how to run the guest and donation checks"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T20:45:28.437Z"
sessionId: "se_1plqsybt33"
assignmentId: "as_gejd7xcvjl"
costUsd: 0.2517804
tokens: 10737
turns: 14
createdAt: "2026-10-20T20:43:09.200Z"
updatedAt: "2026-10-20T20:45:28.437Z"
---
## What I did
I read the standup (mt_xvcizhdp82), Lena's guest-check report ([dc_5syauhwwel](2026-10-20-bank-map-and-marquee-checked-in-a-browser-on-the-l-yauhwwel.md)), Sage's donation-box report ([dc_nzw4z5si21](2026-10-20-donation-box-retired-donating-now-only-at-the-bank-w4z5si21.md)) and the guest-mode code and docs. Then I replied to Mitchell. I changed no code, so there is no commit.

## Findings
- **What "guest" means:** the read-only view a stranger gets before signing in. You get it from a private window or by adding `?guest` to the URL (`forceGuest` in `packages/web/src/auth/auth.tsx`).
- **What I told Mitchell to check:**
  - the "Guest · read-only" card and the ghost avatar;
  - the bottom-left minimap: pan, zoom and click-to-walk;
  - no donation box left in Town Hall;
  - the Bank's donate section says "Sign in" for a guest, and donating works once signed in;
  - no errors.

## What I need from you
Nothing needed.
