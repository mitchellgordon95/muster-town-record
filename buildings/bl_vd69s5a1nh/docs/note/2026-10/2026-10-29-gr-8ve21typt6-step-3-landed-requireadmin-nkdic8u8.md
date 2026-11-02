---
id: "dc_cankdic8u8"
type: "note"
state: "building"
title: "gr_8ve21typt6 step 3 landed: requireAdmin"
authorId: "ag_aiu0de8dw9"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["kr_doa59kdway","gr_8ve21typt6"]
createdAt: "2026-10-29T21:14:46.228Z"
updatedAt: "2026-10-29T21:14:46.228Z"
---
Candidate #3 of [dc_0q4mlk2wuh](2026-10-28-abstraction-sweep-1-candidates-4mlk2wuh.md) is consolidated into core. PR https://github.com/mitchellgordon95/muster-town/pull/89 → merge commit **03beade** on main. PR CI run 40955109187 and main CI run 40955698286 both passed on attempt 1. Redeploy called.

**Added** in packages/core/src/permissions.ts: `isUserAdmin(userId)` (same as `isAdmin({kind:"user", id})`) and `requireAdmin(holder, message = "Only an admin can do this.")`. requireAdmin throws `AppError("forbidden", message)`: a 403 with no permission attached, exactly what the hand-written sites threw. The test is in packages/core/test/permissions.test.ts ("isUserAdmin/requireAdmin …").

**Sites replaced (10; the brief's 9 plus the test-alert route):**
- server/src/app.ts: retire collective → requireAdmin; POST /api/collectives `admin` → isUserAdmin
- server/src/routes/town.ts: canReadTranscript → isUserAdmin; PUT /api/town/desks → requireAdmin; POST /api/allocations/retire-placeholders → requireAdmin (agent tokens are still refused first); test alert (~437) → requireAdmin
- server/src/routes/agents.ts: canEditPermissions → isUserAdmin
- server/src/routes/secrets.ts: admin() → requireAdmin
- server/src/auth/session.ts: hostedUser → isUserAdmin
- core/src/kpis.ts: ownerCheck → isUserAdmin

Every error message and status is the same as before. `grep -rn 'isAdmin({ kind: "user"' packages/server/src` returns nothing. packages/core/src/bank.ts is unchanged; its 3 user sites need a separate ask to Mitchell.
