---
description: "Start Ralph loop in current session"
argument-hint: "PROMPT [--max-iterations N] [--completion-promise TEXT]"
allowed-tools: ["Bash", "Write"]
---

# Ralph Loop

Start a self-referential development loop.

## Step 1: Parse arguments

The raw arguments are:
```
$ARGUMENTS
```

Parse them:
- Extract `--max-iterations N` if present (default: 0 = unlimited)
- Extract `--completion-promise 'TEXT'` if present (default: null)
- Everything else is the PROMPT

## Step 2: Create state file

Use the Write tool to create `.claude/ralph-loop.local.md`:

```yaml
---
active: true
iteration: 1
max_iterations: [N or 0]
completion_promise: "[TEXT]" or null
started_at: "[ISO timestamp]"
---

[THE PROMPT HERE - preserve special characters like | exactly]
```

## Step 3: Confirm

Output:
```
🔄 Ralph loop activated!

Iteration: 1
Max: [N or unlimited]
Promise: [TEXT or none]

⚠️ Loop runs until promise or max-iterations reached.
```

Then show the prompt and start working on it.

## Instructions

Work on the task. When you try to exit, the Ralph loop feeds the SAME PROMPT back. You'll see previous work in files and git history.

**CRITICAL**: If completion promise is set, ONLY output `<promise>TEXT</promise>` when TRUE. Do not lie to escape.
