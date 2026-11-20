# rocket-stack

**Problem:** Agents often mark work as done without showing that it works.

**Solution:** Before claiming done (in the target repo):
- **Mission Map:** how to reach it, control it, and what proof looks like
- **Test Flight:** one real user action that proves success
- **Mission Log:** save proof (action, result, side effect)

Part of [Rocketbase](https://rocketbase.space).

## Skills

- **Rocket Mode** (`rocket-mode`) — Enable the mode, describe the task in plain language. Routes to the other skills; insists on proof before “done.”
- **Mission Control** (`mission-control`) — Prove one mission: update its Mission Map if needed, run a Test Flight, leave a Mission Log.
- **Create Mission Map** (`create-mission-map`) — Create the first Mission Maps (top 3–5) and prove one.
- **Maintain Mission Map** (`maintain-mission-map`) — Fix Mission Map drift when code changes; list missions that need a new proof.

Maps and proof live in the **target repo** (not in this pack):

```
mission-map/<name>/README.md
mission-map/<name>/proof/
```

## Usage

**Prefer Rocket Mode:** enable `/rocket-mode`, then type the task as a normal message (no flags or form fields).

Example: `add login rate limiting`

**Or invoke a skill directly:** `/mission-control login` · `/create-mission-map` · `/maintain-mission-map`  
For `/mission-control`, Surface comes from the map or code; ask only if unclear.

Copy the four skill folders into your agent skills directory.

Repo: https://github.com/rocketbase-space/rocket-stack  
License: MIT
