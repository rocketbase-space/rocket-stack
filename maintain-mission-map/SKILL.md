---
name: maintain-mission-map
description: Keep the Mission Map in sync with the code. Fix drift in routes, commands, selectors, and flows.
---

# Rocketbase Maintain Mission Map

**Goal:** Keep the Mission Map in sync with the code.

**Use:** `/maintain-mission-map`  
No map → `/create-mission-map` first. This skill owns full-map drift; Mission Control only touch-ups one mission mid-flight.  
Update only `mission-map/`. Do not edit skill files. Never delete proof files.

## 1. Check for drift
Compare each `mission-map/<name>/README.md` to the code.  
Changed routes, commands, selectors, or flows → fix.  
Legacy `mission-map/<name>.md` → copy content into `mission-map/<name>/README.md`, create `proof/` if missing, then delete the flat file.

## 2. Update
Fix mismatched entries. Keep existing proof files.  
Don’t run a Test Flight unless asked; list missions to re-prove via `/mission-control <name>`.

## 3. Report

**Output:**
**Changed:** [files] or None  
**Reason:** [one line each] or None  
**Re-prove:** [names] or None

```markdown
**Changed:** mission-map/login/README.md
**Reason:** Login button selector changed from #login to [data-testid="login-button"]
**Re-prove:** login
```

```markdown
**Changed:** None
**Reason:** None
**Re-prove:** None
```
