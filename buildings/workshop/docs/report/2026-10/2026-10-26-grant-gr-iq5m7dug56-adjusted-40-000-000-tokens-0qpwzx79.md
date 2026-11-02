---
id: "dc_hf0qpwzx79"
type: "report"
state: "building"
title: "Grant gr_iq5m7dug56 adjusted: 40,000,000 tokens"
authorId: "system"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["manager-intray","wake:manager-intray:23502:workshop"]
decision: "approve"
decisionNote: "Taken in: gr_iq5m7dug56 adjusted to 40M at 22:17Z; it crossed 100% again at 22:32Z (40.94M after Lena's step 3 session), so the 100% checkpoint as_fa305zaalv runs next and asks Mitchell to continue or adjust once more. Note: migration 037 (step 3, 6105e18) converts the grant to adjusted units on deploy (40M raw → 1,333,333 adj.), so the figure Mitchell sees will change unit."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T22:33:35.495Z"
createdAt: "2026-10-26T22:17:17.896Z"
updatedAt: "2026-10-26T22:33:35.495Z"
---
Written by the town: Mitchell adjusted grant gr_iq5m7dug56 at its checkpoint (event 23502, 2026-10-26 22:17 UTC).

## Summary

Grant gr_iq5m7dug56 "Refactor the whole Bank to track every token type (input, output, cache read, cache write 5m and 1h) end to end; adjusted output tokens derived from them are what donations and every display use; no session dies out of tokens the Bank didn't predict, 7 days running" adjusted by Mitchell: 40,000,000 tokens.

Status funded; 26,023,201 of 40,000,000 tokens spent; key result kr_vyrhhiyotb [on-track] The Bank counts adjusted output tokens (output + weighted input, cache reads, cache writes 5m/1h, from an assumed starting ratio calibrated against real cost) and unexpected out-of-tokens deaths drop to zero over a week.

Acknowledge it with `review` approve once you've taken it in; give any work it calls for with `assign`.
