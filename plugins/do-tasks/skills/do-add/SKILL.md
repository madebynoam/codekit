---
name: do-add
description: Add tasks to your task stack. Alias for /add-task. Triggers on "/do:add my task" or "/do:add task1 | task2". Use --local for project tasks, default is global.
---

# Add Task

Add one or more tasks to your task stack.

## Usage

```
/do:add <task>                    # → global (default)
/do:add <task> --local            # → project-level
/do:add task 1 | task 2           # → multiple tasks
```

## Instructions

Follow the same behavior as `/add-task`:

1. Parse `--local` or `-l` flag (can appear anywhere)
2. Split by `|` for multiple tasks
3. Add to appropriate file:
   - Global: `~/.claude/user-tasks.md`
   - Local: `.claude/tasks.md`
4. Format: `- [ ] <task description>`
5. Confirm and show all pending tasks
