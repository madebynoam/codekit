---
name: sesh:close
description: Prep for session close - save state, update trackers, show next steps
arguments:
  - name: name
    description: Optional session name
    required: false
---

# Session Close

Prepare to close this session by saving state and showing what's next.

## Instructions

### 1. Check for Project Context

Look for `CLAUDE.md` in the current directory or parent directories.
- If found: This is a project with session continuity
- If not found: Treat as standalone session

### 2. Save Session Transcript

Use the same logic as `sesh:save`:
1. Find the current session JSONL in `~/.claude/projects/`
2. Convert to readable markdown
3. Generate summary

**If project has CLAUDE.md:**
- Save to `{project}/sessions/{date}-{name}/`
- Update `CLAUDE.md` with current status

**If no project context:**
- Save to `~/Claude Sessions/{date}-{name}/`

### 3. Update Progress Trackers

If the project has tracking files, update them:
- `interview-progress.md` - mark current position
- Any `TODO` or task files - note where we stopped

### 4. Show Next Steps

Present a summary:

```
## Session Closed

**Saved to:** {path}

### What we did:
- [bullet points from session]

### Next time, pick up with:
- [specific next action]
- [any open questions]

### To resume:
cd {project-path}
claude
# Then say "pick up where we left off" or just start working
```

### 5. Optional: Reflect

Ask if user wants to run `sesh:reflect` for Day One entry:
> Want to capture learnings before closing? (y/n)

If yes, invoke sesh:reflect.

## Examples

**In a project:**
```
/sesh:close anthropic-prep
```
→ Saves to project's sessions folder, updates CLAUDE.md

**Standalone:**
```
/sesh:close
```
→ Saves to ~/Claude Sessions/, suggests a name based on conversation
