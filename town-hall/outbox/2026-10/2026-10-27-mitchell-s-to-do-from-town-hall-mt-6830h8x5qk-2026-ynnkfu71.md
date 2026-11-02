---
id: "dc_yjynnkfu71"
type: "request"
state: "building"
title: "Mitchell's to-do from town hall mt_6830h8x5qk (2026-10-27): four Fund presses, one reject, two key-result marks, one token re-issue"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["other"]
requestStatus: "done"
claimedByUserId: "us_1la74k332n"
createdAt: "2026-10-27T17:47:06.699Z"
updatedAt: "2026-10-27T22:53:14.629Z"
---
You asked at the end of the town hall for your to-dos in the outbox with What, Why and How. Here they are (notes: [dc_evzrmyl3pp](../../../library/meeting-notes/2026-10/2026-10-27-town-hall-town-hall-notes-zrmyl3pp.md)).

1. WHAT: Press Fund on four proposals in the Town Hall in-tray: gr_tvt32g9xly (Workshop, member funding, 300k adj.), gr_rdyrjzclfe (Onboarding, hosted collectives, 1,000,000 adj.), gr_gi5jbgzv4k (Bank Transparency, finance page, 1.2M adj.), gr_z9xj51uox3 (Code Legibility, architecture docs, 400k adj.). WHY: you approved each in the meeting; nothing runs until Fund is pressed (only a human can). HOW: Town Hall → in-tray → each proposal row → Fund (leave the token number as asked). Leave gr_f5bmciloqy (starter brief) open: the visitor-agent review comes first.

2. WHAT: Reject gr_ph4kky6r99 (Prod, token rotation, 600k). WHY: you said to skip it. HOW: same in-tray row → Reject, note "skipped".

3. WHAT: Mark key result kr_z9lcfnvt94 (Prod, stress test) met. WHY: you acknowledged the stress test done; only a human marks met. HOW: Prod building board → key results → kr_z9lcfnvt94 → status met; evidence is Cleo's rollup #8. (Once the Workshop's early grant close is live, Cleo also closes gr_wqnunw5yd8 with its surplus; that will show up in your in-tray for a second met/missed click.)

4. WHAT: Delete kr_tzg9en02dh from the Onboarding goal. WHY: the README-walk key result was cut last town hall; only a human deletes one. HOW: Onboarding board → key results → kr_tzg9en02dh → delete.

5. WHAT: Re-issue the desk GitHub token in Town Hall → Secrets with Workflows read and write, on top of Contents, Pull requests and Metadata. WHY: desks cannot push files under .github/workflows without it, so Code Legibility cannot add its CI step. HOW: GitHub → Settings → Developer settings → Fine-grained tokens → the desk token (or a new one for the same repo) → Repository permissions: Contents RW, Pull requests RW, Metadata R, Workflows RW → copy → Town Hall → Secrets → replace the value → keep it granted to the desks. Mara then merges PR #58 herself.

6. WHAT: Run Cleo's Claude Code prompt for the Prod backup bucket, key and restore drill when it arrives (Cleo files it in Prod). WHY: backups need a bucket and a key only you can create. HOW: Cleo's doc will contain the prompt to paste.

Done already: FLY_DESKS_ACCESS_TOKEN granted town-wide (Root is running the image redeploy now); FLY_STRESS_TOKEN revoked.
