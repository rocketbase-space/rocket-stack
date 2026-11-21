---
name: ground-control
description: Track code quality across the whole repo. Keep a Space Debris list with file:line evidence; pick the top 1–3 to fix next.
---

# Rocketbase Ground Control

**Goal:** Keep code quality on track across the whole repo.

**Use:** `/ground-control`  
Fix items via Rocket Mode (Ship). The next scan marks them **Fixed**.  
Write only `ground-control/debris.md` in the target repo. Do not change app code. Do not edit skill files.

## 1. Scan
Read the whole repo (skip vendored, generated, and build output). Look for:

- **Duplicate** — same logic in 2+ places
- **Dead code** — unused files, functions, exports, flags
- **Missing tests** — important code with no test
- **Oversized** — files over ~400 lines, functions over ~50 lines
- **Fragile** — swallowed errors, unchecked input, hardcoded secrets
- **Debris** — debug output, commented-out code, stray TODOs

Every item needs evidence: `file:line`. No evidence → no item.

## 2. Update the Space Debris list
Read `ground-control/debris.md` if it exists.  
Re-check every **Open** item: gone → **Fixed** (with date). Still there → keep, update `file:line`.  
Add new items with the next ID. Never delete items; history is the trend.

Severity: **High** (bugs or security risk) · **Medium** (slows every change) · **Low** (cosmetic).  
Status: **Open** · **Fixed** · **Accepted** (kept on purpose, with reason).

```markdown
# Space Debris
Last scan: 2026-11-21 · Open: 2 (was 3) · Trend: better

| ID | Type | Evidence | Severity | Status |
| --- | --- | --- | --- | --- |
| D1 | Duplicate | src/auth/login.ts:30, src/auth/signup.ts:28 — same email validation | Medium | Open |
| D2 | Missing tests | src/billing/invoice.ts:12 — no test for invoice totals | High | Open |
| D3 | Debris | src/app.ts:88 — console.log of request body | High | Fixed 2026-11-21 |
| D4 | Oversized | src/admin/panel.tsx:1 — 900 lines | Low | Accepted: legacy, rewrite planned |
```

Trend: fewer Open than last scan → better · more → worse · same or first scan → steady.

## 3. Next
Pick the top 1–3 Open items: highest severity first, then smallest fix.  
Do not fix them here. Hand each off as a plain task for Rocket Mode, with the mission it touches from `mission-map/` (closest one; every fix still needs a Test Flight), e.g. `fix D2: add tests for invoice totals (billing)`.

## 4. Report

**Output:**
**Open:** n (was n)  
**Trend:** better / worse / steady  
**Next:** [IDs + one line each] or None  
**Proof:** ground-control/debris.md

```markdown
**Open:** 2 (was 3)
**Trend:** better
**Next:** D2 add tests for invoice totals · D1 share email validation
**Proof:** ground-control/debris.md
```

---

**Tagline:**  
The mission succeeds only when proven.
