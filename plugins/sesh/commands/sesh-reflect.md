---
name: sesh:reflect
description: End-of-session reflection - learnings and feelings to Day One
arguments:
  - name: session-name
    description: Optional session name (defaults to current date)
    required: false
---

Guide an end-of-session reflection and save to Day One or a local markdown file.

## Instructions

### 1. Determine storage backend

Read `~/.claude/journal-config.md` to determine where reflections are saved.

- If the config file exists with a `learned_journal_id`, use Day One.
- If the config file exists with `learned_backend: markdown`, use the configured `learned_file` path.
- If the config file doesn't exist, check if Day One MCP is available:
  - **If available**: List journals, ask the user which to use, and save the config (see `/learned` command for setup flow).
  - **If not available**: Ask where to save reflections (default: `~/.claude/reflections.md`) and save the config.

### 2. Analyze the session
Review what was accomplished:
- What technical concepts were used or discovered?
- What soft skills were practiced (communication, problem-solving)?
- What workflows or patterns were established?
- What mistakes were made and corrected?

### 3. Present learnings
Show the user what you observed they learned, numbered for easy reference:

```
Based on this session, here's what I think you learned:

**Technical:**
1. [specific technical learning]
2. [another learning]

**Process/Soft Skills:**
3. [workflow or communication learning]

**Patterns Established:**
4. [reusable patterns or commands created]
```

Ask: "Want to keep, edit, or add? (e.g., 'drop 2', 'edit 3: [new text]', 'add: [learning]')"

### 4. Ask for feelings
After learnings are confirmed, ask:

"How do you feel about the work? (e.g., empowered, frustrated, curious, accomplished)"

Let them express freely - one word or a sentence.

### 5. Save the reflection

Format the entry:

```markdown
# Session: [Session Name]

**Path:** ~/Claude Sessions/[session-folder]/

## What I Learned

### Technical
- [learning 1]
- [learning 2]

### Process
- [learning 1]

## How I Feel
[Their feeling and any elaboration]

## Session Context
[1-2 sentence summary of what was built/fixed]
```

**If using Day One:**
Create the entry in the configured journal. Tags: `session-reflection` plus any relevant project tags.

**If using markdown:**
Append the entry (preceded by a `---` separator) to the configured file. Include tags as `**Tags:** #session-reflection #project-name`.

### 6. Confirm
- If Day One: show the view link and confirm saved
- If markdown: show the file path and confirm saved

## Notes
- Keep learnings specific and actionable, not generic
- Feelings can be brief - even one word is valuable
- The session path links back to technical details if needed
- If no session was saved yet, note the current working directory instead

Session name: $ARGUMENTS
