---
name: mission-control
description: Prove a mission succeeds. Write a Mission Map entry, run a Test Flight, capture proof.
---

# Rocketbase Mission Control

**Goal:** Prove the mission succeeds.

**Use:** `/mission-control <name>` (kebab-case, e.g. `/mission-control login`).  
Surface from the map (`Surface: UI|API|CLI`), or from the code if no map yet. Ask only if unclear.

No map yet → `/create-mission-map`. Full drift scan → `/maintain-mission-map`.  
Write only under `mission-map/` in the target repo. Do not edit skill files.

## 1. Briefing
Read the code. Ask the user only what it does not show (max 3). If unreachable, note assumptions and proceed.  
Resolve Surface as above. Mission names: kebab-case.

## 2. Flight Procedure
- **System Startup** — reuse if already usable. Otherwise look for a start command in the repo (package.json scripts, Makefile, README, or Dockerfile). If none is obvious, ask once. Don’t duplicate processes.
- **Ready Check** — mission is running and accepts input on this surface (UI interactable and shows a result / API reachable and returns a response / CLI runnable and produces output). Note port or version if known.
- **Test Case** — one real user action that proves success
- **Mission Log** — save proof under `mission-map/<name>/proof/`. UI: screenshot. API: response. CLI: output. Show action, result, and side effect. On fail, still capture proof when possible (`Proof: None` only if impossible).
- **Post-flight Cleanup** — stop what you started. Keep proof.

## 3. Mission Map
One folder per mission before Test Flight:

`mission-map/<name>/README.md`  
`mission-map/<name>/proof/`

Put the Test Case under “How to control it”. Exact commands, selectors, or routes. Gotchas: `- None` if empty.

```markdown
# [Name]
Surface: UI | API | CLI

## What it does
## How to reach it
## How to control it
[Exact command, selector, or route]
## Proof required
## Gotchas
- None
```

Surface is metadata under the title (not a section). First real section is “What it does”.

Example (`mission-map/login/README.md`):
```markdown
# Login
Surface: UI

## What it does
Allows a user to sign in with email and password.

## How to reach it
Open the app and go to /login.

## How to control it
1. Enter email and password
2. Click Login
Selector: [data-testid="login-button"]

## Proof required
Screenshot of the dashboard after redirect (proof/dashboard.png).

## Gotchas
- Invalid credentials must show an error
```

API — How to control it:
```markdown
POST /api/login
Body: { "email": "...", "password": "..." }
```

CLI — How to control it:
```markdown
rocketbase login --email user@example.com
```

## 4. Test Flight
Run end-to-end. Fail → stop and report.

## 5. Keep current
If the controls you used no longer match the map, update **only** `mission-map/<name>/` for the mission under test.  
Do not create, edit, rename, or delete any other mission’s map or proof.  
Do not rewrite this skill.

**Output:**
**Result:** Pass / Fail  
**Proof:** path or None  
**Note:** one line  
**Updated:** map path or None

```markdown
**Result:** Pass  
**Proof:** mission-map/login/proof/dashboard.png  
**Note:** User redirected to dashboard after valid login.  
**Updated:** None
```

```markdown
**Result:** Fail  
**Proof:** mission-map/login/proof/error.png  
**Note:** Error message did not appear.  
**Updated:** None
```

---

**Tagline:**  
The mission succeeds only when proven.
