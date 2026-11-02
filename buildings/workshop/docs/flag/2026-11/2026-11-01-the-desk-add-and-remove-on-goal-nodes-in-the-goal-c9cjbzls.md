---
id: "dc_42c9cjbzls"
type: "flag"
state: "building"
title: "the desk add and remove on goal nodes in the goal editor do not handle long building names well."
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag dc_42c9cjbzls (goal editor, picked up 2026-11-02 in 1:1 mt_a64faz59yr): two asks, one PR each or one PR with both.\n1. The desks −/+ badge on a goal node in the goal editor canvas does not handle long building names: the name overflows or pushes the controls out. Fix the node layout (truncate with an ellipsis and a title tooltip, or wrap, keep the −/+ controls aligned); check with a long name like \"People who would use Muster Town know…\" (bl_6ifesdbah3) and in Fit all at low zoom.\n2. Going from 0 to 1 desks on a goal node creates a building named after the goal text verbatim. Instead run a short Haiku pass (the Bank's cheap model, one call, a few tokens) that names the building something reasonable (short, a place name, like \"Onboarding\" or \"Bank Transparency\"), with the goal text as the fallback when the call fails or the Bank can't run it. Record the call like other host SDK calls (funded through the Bank, booked). Show the chosen name in the editor as soon as the building exists.\nTests for the naming fallback; merge if green, redeploy, guest live-check the editor (long name, and a 0→1 desks creation if you can do it on a throwaway node), add a Shipped candidate to dc_7lpbltjy1j. Topic pages: dc_hsq0e5a587 (goal editor), dc_e5xzfn81ge (map from the tree)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T02:17:01.088Z"
flagPos: {"x":78,"y":5}
pickedUpAt: "2026-11-02T02:16:49.135Z"
pickedUpBy: "ag_mh0qidzgw6"
createdAt: "2026-11-01T22:22:21.945Z"
updatedAt: "2026-11-02T02:17:01.088Z"
---
the desk add and remove on goal nodes in the goal editor do not handle long building names well.

also, rather than setting the building name to the goal verbatim, let's run a short haiku pass to name the building something reasonable when going from 0 to 1 desks
