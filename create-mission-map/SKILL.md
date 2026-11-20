---
name: create-mission-map
description: Generate a Mission Map from the repo (top 3–5 missions); prove one with Mission Control.
---

# Rocketbase Create Mission Map

**Goal:** Generate a Mission Map from the repo.

**Use:** `/create-mission-map`  
Prove one mission with `/mission-control <name>` after writing. No Mission Control → **Proven:** None.  
Drift later → `/maintain-mission-map`. Write only under `mission-map/`. Do not edit skill files.

## 1. Interview the repo
Read routes, commands, menus, and docs.  
Ask the user only what the code does not show (max 3). If unreachable, note assumptions and proceed.  
Surface: UI, API, or CLI. Names: kebab-case.

## 2. Write the map
Create entries for the top 3–5 missions. Prefer: happy paths first, then auth, then fragile or edge flows. Skip admin or internal tools unless they are the product.

`mission-map/<name>/README.md`  
`mission-map/<name>/proof/`

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

## 3. Prove it
Pick one mission. Run `/mission-control <name>` end-to-end.  
After the Test Flight, check that the map entry still matches what you actually did. Update it if needed.

## 4. Report

**Output:**
**Created:** [names]  
**Proven:** [name] or None  
**Proof:** path or None  
**Note:** one line

```markdown
**Created:** login, signup, logout
**Proven:** login
**Proof:** mission-map/login/proof/dashboard.png
**Note:** Maps written; login Test Flight passed.
```
