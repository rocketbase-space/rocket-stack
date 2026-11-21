---
name: pre-flight-check
description: Code review of your own change, as a strict peer reviewer would, before claiming done. Fixed checklist, every finding with file:line, Go / No-go before the Test Flight.
---

# Rocketbase Pre-Flight Check

**Goal:** Review your own code like a peer would, before the Test Flight.

**Use:** `/pre-flight-check <name>` (the mission the change belongs to, e.g. `/pre-flight-check login`).  
Run it before the Test Flight, so the flight proves the final code.  
Go → `/mission-control <name>`. Issues outside your change → don't fix them; note them for the next `/ground-control`.  
Write only `mission-map/<name>/proof/pre-flight.md` (create `proof/` if missing) and the code of your own change. Do not edit skill files.

## 1. Briefing
Read the task and your diff (`git diff` against where you started; untracked files too).  
Review only lines you changed.

## 2. Checklist
Run every check. Each finding: `file:line` + what you fixed or why it is accepted.

| Check | Ask |
| --- | --- |
| **Brief** | Does the change do what was asked — no more, no less? |
| **Tests** | Is the new behavior tested? Do existing tests pass? |
| **Errors** | Bad input, empty, timeout, failed call: handled, not swallowed? |
| **Security** | Secrets, injection, auth checks, user data in logs? |
| **Readability** | Clear names, small functions, no duplicated logic? |
| **Debris** | Debug output, commented-out code, unused code, stray TODOs? |

Status per check: **Pass** (nothing found) · **Fixed** (changed the code) · **Accepted** (kept, with reason) · **Open** (unresolved).  
Any **Open** → **No-go**: stop and report. Otherwise **Go**. Pass with nothing to cite → Evidence `None`.

## 3. Mission Log
Save `mission-map/<name>/proof/pre-flight.md`; replace it each run.

```markdown
# Pre-Flight Check: login
Change: Rate limit on POST /api/login

| Check | Status | Evidence |
| --- | --- | --- |
| Brief | Pass | src/auth/login.ts:42 — 5 attempts/min per IP, as asked |
| Tests | Fixed | test/login.test.ts:88 — added test for 429 after 5 attempts |
| Errors | Pass | src/auth/login.ts:51 — limiter store down → request allowed, error logged |
| Security | Pass | src/auth/login.ts:44 — keyed by IP, no email in logs |
| Readability | Pass | None |
| Debris | Fixed | src/auth/login.ts:60 — removed console.log |

**Result:** Go
```

## 4. Report

**Output:**
**Result:** Go / No-go  
**Fixed:** n  
**Accepted:** n  
**Open:** n  
**Proof:** path  
**Note:** one line (on No-go: `file:line` per open item)

```markdown
**Result:** Go
**Fixed:** 2
**Accepted:** 0
**Open:** 0
**Proof:** mission-map/login/proof/pre-flight.md
**Note:** Test and console.log fixed; ready for the Test Flight.
```

---

**Tagline:**  
The mission succeeds only when proven.
