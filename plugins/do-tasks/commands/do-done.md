---
name: do:done
description: Mark a task as complete. Alias for /done-task. Triggers on "/do:done 3" or "/do:done fix bug". Accepts task number or partial text match.
arguments:
  - name: task
    description: Task number or partial text match
    required: true
---

# Mark Task Done

Mark a task as complete and show remaining tasks.

## Usage

```
/do:done 3                  # by number
/do:done fix highlight      # by text match
/do:done 2 --global         # specific stack
```

## Instructions

Follow the same behavior as `/done-task`:

1. Parse `--local`/`-l` or `--global`/`-g` flag
2. Find task by number or text search
3. Update file:
   - Change `- [ ] Task` to `- [x] ~~Task~~`
   - Move to `## Completed` section
4. Confirm and show remaining tasks
