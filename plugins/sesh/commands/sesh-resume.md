---
name: sesh:resume
description: Pick up from last session - read context files and show where we left off
arguments: []
---

# Session Resume

Pick up where the last session left off by reading project context.

## Instructions

### 1. Look for CLAUDE.md

Check current directory and parent directories for `CLAUDE.md`.

**If found:**
- Read it completely - this is the project context
- Note the "Current Status" and "Next Up" sections
- Check for linked files (interview-progress.md, etc.)

**If not found:**
- Check `~/.claude/goals.md` for general context
- Check `~/.claude/user-tasks.md` for pending tasks
- Look for recent sessions in `~/Claude Sessions/`

### 2. Read Progress Trackers

If CLAUDE.md references tracking files, read them:
- `interview-progress.md` - where are we in a multi-step process?
- `README.md` - project overview
- Any task lists or TODO files

### 3. Check Last Session

Look for the most recent session in:
1. `{project}/sessions/` (if project)
2. `~/Claude Sessions/` (if standalone)

Read the `summary.md` to understand what was accomplished.

### 4. Present Context

Show a brief summary:

```
## Resuming: {project name}

**Last session:** {date}
**What we did:**
- [key points from summary]

**Where we left off:**
- {current position from trackers}

**Next up:**
- {next action from CLAUDE.md or trackers}

Ready to continue?
```

### 5. Offer Options

```
What would you like to do?
1. Continue from where we left off
2. Check /do:coach for priorities
3. Something else
```

## Examples

**In a project directory:**
```
/sesh:resume
```
→ Reads CLAUDE.md, shows progress, reminds where you left off

**In any directory:**
```
/sesh:resume
```
→ Checks goals, tasks, offers to run do:coach
