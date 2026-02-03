---
name: dev:worktrees
description: List active git worktrees and branches for the current project
arguments: []
---

List all git worktrees and their branches for the current repository.

## Instructions

### 1. List all worktrees
Run:
```bash
git worktree list
```

### 2. For each worktree, gather info
For each worktree path, check:
- Current branch name
- Uncommitted changes: `git -C <path> status --porcelain`
- Commits ahead/behind trunk: `git -C <path> rev-list --left-right --count origin/trunk...HEAD`

### 3. Format output
Present a clean summary table:

```
## Worktrees for [repo-name]

| Path | Branch | Status | vs trunk |
|------|--------|--------|----------|
| /path/to/main | trunk | clean | - |
| /path/to/feature | add/feature-x | 2 changes | +3 / -1 |
```

### 4. If only main worktree exists
Show the current branch info and mention:
- Use `git worktree add <path> <branch>` to create parallel working directories
- Worktrees let you work on multiple branches simultaneously without stashing
