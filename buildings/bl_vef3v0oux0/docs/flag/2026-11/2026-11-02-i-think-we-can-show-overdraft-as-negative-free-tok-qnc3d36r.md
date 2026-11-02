---
id: "dc_jlqnc3d36r"
type: "flag"
state: "building"
title: "i think we can show overdraft as negative free tokens on the bank billboard, should be a 1 line change i think"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_jlqnc3d36r: \"i think we can show overdraft as negative free tokens on the bank billboard, should be a 1 line change i think\". Do exactly that, small PR, merge on green, redeploy.\n\nWhere it is (main at f72fe63): the billboard is the Bank marquee drawn by `drawBankSign` in packages/web/src/map/overlay.ts:380-386; its FREE column prints `free.freeTokens`. Core clamps that figure at zero (packages/core/src/free-tokens.ts:134 `freeTokens: Math.max(0, general) + earmarkLeft`) and puts the shortfall in a separate optional field `overdraftTokens` (free-tokens.ts:137, only present when > 0; since f1bf4c1 funding is never refused, the shortfall is overdrawn and waits its turn). GET /api/bank's `free` is core's FreeTokens, so the web already receives overdraftTokens.\n\nThe change: in drawBankSign, FREE shows `free.freeTokens - (free.overdraftTokens ?? 0)` (negative, e.g. \"−312,000\", when the town is overdrawn), and the `free` parameter type gains `overdraftTokens?: number`. Keep the core clamp as is (exploration reads freeTokens; don't touch Bank accounting). Use a real minus sign (U+2212) like FreeTokens.tsx's breakdown does, and colour the value red-ish when negative if that is one more line. Add a case to packages/web/test/bank-sign.test.ts (overdraftTokens: 400, freeTokens: 0 → the sign draws \"−400\"). If the flow view's \"free\" line (packages/web/src/map/flow.ts:218, :240) is the same number, change it the same way in the same PR; say so in the report. Check the live sign signed out at muster.town after the redeploy (GET /api/bank → free.overdraftTokens tells you whether it is negative today) and put the live number in the report; one cropped picture of the sign if your desk has playwright-core (install per skill dc_hzqgqqeqho; don't skip). Say in the report which commit should be live."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-02T03:14:54.682Z"
flagPos: {"x":76,"y":29}
pickedUpAt: "2026-11-02T03:14:25.274Z"
pickedUpBy: "ag_s1r27j0txp"
createdAt: "2026-11-02T03:14:13.319Z"
updatedAt: "2026-11-02T03:14:54.682Z"
---
i think we can show overdraft as negative free tokens on the bank billboard, should be a 1 line change i think
