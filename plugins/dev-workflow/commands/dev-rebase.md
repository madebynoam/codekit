---
name: dev:rebase
description: Safely rebase current branch with trunk, handling stash and push
arguments:
  - name: push
    description: Auto push after rebase (yes/no)
    required: false
---

Safely rebase the current branch with trunk.

## Instructions

### 1. Check current state
- Show current branch name
- Check for uncommitted changes
- Show how many commits ahead/behind trunk

### 2. Handle uncommitted changes
If there are uncommitted changes:
- Stash them automatically
- Note what was stashed
- Will restore after rebase

### 3. Fetch and rebase
```bash
git fetch origin trunk
git rebase origin/trunk
```

### 4. Handle conflicts (if any)
If conflicts occur:
- List the conflicting files
- Ask user how to proceed:
  - Help resolve conflicts
  - Abort rebase
- Do NOT auto-resolve without user input

### 5. Restore stashed changes
If changes were stashed:
- Pop the stash
- Report any stash conflicts

### 6. Push (if requested or ask)
If rebase succeeded:
- If `push` argument is "yes", push with `--force-with-lease`
- Otherwise, ask user if they want to push
- Explain that force push is needed because history changed
- Use `--force-with-lease` for safety (fails if someone else pushed)

### 7. Report summary
Show:
- Rebased with trunk
- X commits replayed
- Stash restored (if applicable)
- Pushed to remote (if applicable)

## Safety Notes
- Always use `--force-with-lease` not `--force`
- Never rebase shared/main branches
- Warn if branch appears to be a main branch

Push preference: $ARGUMENTS
