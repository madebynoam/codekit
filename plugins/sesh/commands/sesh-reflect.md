---
name: sesh:reflect
description: End-of-session reflection - learnings and feelings to Day One
arguments:
  - name: session-name
    description: Optional session name (defaults to current date)
    required: false
---

Guide an end-of-session reflection and save to Day One.

## Instructions

### 1. Analyze the session
Review what was accomplished:
- What technical concepts were used or discovered?
- What soft skills were practiced (communication, problem-solving)?
- What workflows or patterns were established?
- What mistakes were made and corrected?

### 2. Present learnings
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

### 3. Ask for feelings
After learnings are confirmed, ask:

"How do you feel about the work? (e.g., empowered, frustrated, curious, accomplished)"

Let them express freely - one word or a sentence.

### 4. Create Day One entry
Use the Day One MCP tool to create an entry in the "Learned" journal:

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

Tags: `session-reflection` plus any relevant project tags (e.g., `a4a`, `calypso`)

### 5. Confirm and share link
After creating the entry:
- Show the Day One view link
- Confirm the reflection was saved

## Notes
- Keep learnings specific and actionable, not generic
- Feelings can be brief - even one word is valuable
- The session path links back to technical details if needed
- If no session was saved yet, note the current working directory instead

Session name: $ARGUMENTS
