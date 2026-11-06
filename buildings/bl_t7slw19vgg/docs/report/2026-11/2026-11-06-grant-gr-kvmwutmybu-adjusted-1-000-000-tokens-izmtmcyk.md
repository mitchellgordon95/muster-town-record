---
id: "dc_6hizmtmcyk"
type: "report"
state: "building"
title: "Grant gr_kvmwutmybu adjusted: 1,000,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:136355:bl_t7slw19vgg"]
decision: "approve"
decisionNote: "Taken in: Mitchell adjusted gr_kvmwutmybu to 1,000,000 tokens (821,388 spent, 178,612 left). Open key results kr_mmdday2x7z and kr_z4junko6nt are both in PR #350 (step 4, draft since 11-04); its parked continuation is re-queued with rebase instructions."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-06T04:20:46.885Z"
createdAt: "2026-11-06T04:18:15.740Z"
updatedAt: "2026-11-06T04:20:46.885Z"
---
Written by the town: Mitchell adjusted grant gr_kvmwutmybu at its checkpoint (event 136355, 2026-11-06 04:18 UTC).

## Summary

Grant gr_kvmwutmybu "Every panel reads as one design: interface text is readable at a glance (no dim grey labels or timestamps) and panels share one small type scale and one palette." adjusted by Mitchell: 1,000,000 tokens.

Status funded; 821,388 of 1,000,000 tokens spent; key results kr_w9t4cey0l2 [claimed] No dim interface text: the census shows 0 interface text lines under WCAG 4.5:1 contrast (3:1 for large text) on the 10 guest views (8 panels + home page + how-it-works) at 1280×800 and 390×844 (live a84ed22: 2–14 per laptop panel view, 40 in total).; kr_68eg5yskoo [claimed] One type scale: each of the 10 guest views shows ≤6 distinct font sizes at both sizes (live a84ed22: 7–13 on the 8 panels), and the three web CSS files declare font sizes only through ≤6 scale variables (live: 19 distinct px values).; kr_qge1yo1lmi [claimed] One palette: the web CSS declares colour only through :root tokens (≤24 tokens; live a84ed22: 15 tokens plus ~135 stray hex values across styles.css, hiw.css, home.css), and a repo check fails CI if a hex colour appears outside the :root block.; kr_mmdday2x7z [on-track] Signed-in views match: the census run on the mock town signed in (goal tree, Town Hall in-tray, review deck, Bank interior tabs, 1:1, planning desk) shows 0 low-contrast lines and ≤6 font sizes per view at both sizes.; kr_z4junko6nt [not-started] The system is written down where a human can see it: the manual gets a Design section showing each colour token and type step as a named swatch or sample, and the close report carries one contact sheet of the 10 guest views before and after..

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
