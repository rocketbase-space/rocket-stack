---
name: rocket-mode
description: Turn on Rocket Mode, describe the task in plain language. Routes to Mission Map / Pre-Flight Check (peer code review) / Test Flight / Ground Control work and insists the mission is proven.
---

# Rocket Mode

**Goal:** Pick the mission. The mission succeeds only when proven.

**Use:** Turn on `/rocket-mode`, then write the task in plain language. No flags or form fields.

**Depends on:** `mission-control`, `create-mission-map`, `maintain-mission-map`, `pre-flight-check`, `ground-control`.  
Mission Map + proof in the **target** repo: `mission-map/<name>/README.md` + `proof/`. Space Debris: `ground-control/debris.md`.  
Do not edit skill files. Never delete proof (pre-flight.md is overwritten each run).

## 1. Briefing
Read the task. Choose one playbook (internal — the user does not name it).  
Prefer existing Mission Map entries.  
Ask at most 3 times; else note assumptions. Surface from the map or code. Names: kebab-case.

## 2. Flight plan (internal)

| Playbook | When | Route |
| --- | --- | --- |
| **Map first** | No useful Mission Map, or none for this mission | `/create-mission-map` → `/mission-control <name>` (one Test Flight) |
| **Prove** | Need Pass/Fail | `/mission-control <name>` (that map only) |
| **Drift** | Code changed; Mission Map may lie | `/maintain-mission-map` → `/mission-control <name>` for each **Re-prove** |
| **Ship** | Build/change a mission | Implement → `/pre-flight-check <name>` → `/mission-control <name>` (only this mission’s map + Test Flight) |
| **Fix fail** | Last Test Flight failed | Reproduce the fail → change the code → `/pre-flight-check <name>` → `/mission-control <name>` |
| **Ground control** | Code quality or cleanup | `/ground-control` → Ship the top item the user picks |

**Default:** Prove if the mission is clear; else Map first.

## 3. Rules
- Rocket Mode **routes only**: it does not write Mission Maps, review code, or run Test Flights itself — hand off to the skills below.
- Read and follow each routed skill end-to-end; do not rewrite it.
- Claiming done → a Test Flight with proof via `/mission-control` (Pass/Fail + path(s) or `None`).
- You changed code (Ship, Fix fail) → `/pre-flight-check <name>` before the Test Flight. No-go → stop; not done.
- Only that mission’s map may change (unless Drift). Ship **writes app code**, then hands off to prove (one mission per run).

## 4. Mission Log

**Output:**
**Playbook:** …  
**Next:** slash command(s) used  
**Result:** …  
**Proof:** path(s) or None  
**Note:** one line

```markdown
**Playbook:** Ship
**Next:** /pre-flight-check login → /mission-control login
**Result:** Pass
**Proof:** mission-map/login/proof/pre-flight.md, mission-map/login/proof/dashboard.png
**Note:** Rate limit added; Pre-Flight Check Go; login Test Flight passed.
```

---

**Tagline:**  
The mission succeeds only when proven.
