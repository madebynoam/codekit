---
name: sesh:save
description: Save the current session with both raw transcript and summary to ~/Claude Sessions/
arguments:
  - name: name
    description: A short descriptive name for the session (optional)
    required: false
---

Save this session to `~/Claude Sessions/` with both a raw transcript and summary.

## Instructions

### 1. Determine the session name
- If a name argument was provided, use it (convert spaces to hyphens, lowercase)
- If no name provided, create a brief 2-4 word summary of the main topic
- Format: `YYYY-MM-DD-{name}` (e.g., `2026-01-20-a4a-responsive-styling`)

### 2. Create the session folder
```
~/Claude Sessions/{session-name}/
├── summary.md    # Key insights, decisions, outcomes
└── raw.md        # Full conversation transcript
```

### 3. Find and convert the raw transcript
- Find the current session's JSONL transcript in `~/.claude/projects/`
- Look for the most recently modified `.jsonl` file matching the current working directory
- Convert JSONL to readable markdown format:
  - Parse each JSON line
  - Extract user and assistant messages
  - Format as `**User:** {message}` and `**Assistant:** {message}`
  - Skip system messages and tool internals
- Save as `raw.md`

### 4. Generate the summary
Create `summary.md` with:
- Header: `# Session: {descriptive title}`
- Date and working directory
- **Summary**: 2-3 paragraph overview of what was accomplished
- **Key Work Done**: Bullet points of main tasks/changes
- **Technical Notes**: Any important insights or decisions
- **Files Modified**: List of files changed (if applicable)
- **Commits Made**: List of commits (if applicable)

### 5. Confirm completion
Report:
- Full path to the session folder
- Confirmation that both files were created

## Example Output Structure

```markdown
# summary.md
# Session: A4A Responsive Styling Updates

**Date:** 2026-01-20
**Directory:** /Users/name/project

## Summary
[2-3 paragraphs]

## Key Work Done
- [bullet points]

## Files Modified
- path/to/file.tsx
```

```markdown
# raw.md
# Session Transcript

**User:** [first message]

**Assistant:** [response]

**User:** [next message]
...
```

User provided name argument: $ARGUMENTS
