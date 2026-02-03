---
name: do-list
description: List all pending tasks from global and project task stacks. Alias for /tasks. Triggers on "/do:list", "/do:tasks", or "show my tasks".
---

# List Tasks

Show all pending tasks from both global and project stacks.

## Usage

```
/do:list
/do:tasks
```

## Instructions

Follow the same behavior as `/tasks`:

1. Read both task files:
   - Global: `~/.claude/user-tasks.md`
   - Local: `.claude/tasks.md` (if exists)
2. Display pending tasks numbered:

```
Tasks (X pending):

Global:
  1. First task
  2. Second task
  ...

Local:
  X. Project task
  ...
```

3. Show completed count if any exist
