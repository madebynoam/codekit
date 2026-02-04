---
name: do:learned
description: Learned - Quick Journal Entry
---

# Learned - Quick Journal Entry

Log something you learned — to Day One or a local markdown file.

## Usage
```
/learned <what you learned> #tag
```

## Examples
```
/learned Claude has /resume command to get back to where you were #ai-nyc
/learned Git rebase -i can squash commits #git
/learned Use cmd+k to clear terminal #terminal
```

## Instructions

Parse the user's input from: $ARGUMENTS

### 0. Determine storage backend

Check if the Day One MCP tool is available in this session.

- **If Day One MCP is available**: Check for `~/.claude/journal-config.md`. If it exists, read the `learned_journal_id` value. If it doesn't exist, list available journals with the Day One MCP, ask the user which journal to use for learnings, and save the choice to `~/.claude/journal-config.md` in this format:
  ```markdown
  # Journal Configuration
  learned_journal_id: <id>
  ```
- **If Day One MCP is NOT available**: Ask the user where to save learnings:
  - Option 1: `~/.claude/learned.md` (Recommended)
  - Option 2: A custom file path
  Save their choice to `~/.claude/journal-config.md` as:
  ```markdown
  # Journal Configuration
  learned_backend: markdown
  learned_file: <path>
  ```

Once configured, use the stored config for all future calls (don't ask again).

### 1-2. Parse input

1. Extract the main message (everything before any hashtags)
2. Extract all tags if present (words after #, without the # symbol)

### 3. Smart tag matching and suggestion

- **If using Day One**: Query recent entries from the Learned journal to get a list of existing tags
- **If using markdown**: Read the markdown file and extract existing `#tags` from entries
- **If user provided tags**: check if they closely match existing tags (typo detection). If a tag looks like a typo (e.g., "ai-ny" instead of "ai-nyc"), suggest the correct one
- **If user provided NO tags**: analyze the content and suggest 2-4 relevant tags from the existing tag list. Include these suggested tags in the AskUserQuestion step so the user can select which ones to apply (or skip all)

### 4. Generate TWO versions of the entry

- **Original**: The message exactly as the user typed it
- **Refined**: A cleaner, more complete version that:
  - Fixes typos and grammar
  - Adds context that would help with future recall
  - Makes it self-contained (would make sense if you read it months later)
  - Keeps it concise (1-3 sentences max)

### 5. Present options

Use AskUserQuestion to present options:
- **Question 1 (Entry version)**:
  - Option 1: The refined version (recommended)
  - Option 2: The original text (as written)
  - Option 3: Both versions together
- **Question 2 (Tags)** - always include this question as multi-select:
  - Show the top 3 most relevant existing tags based on content, ordered by relevance
  - Add "Skip tags" as the 4th option
  - User can select multiple tags, or choose "Other" to type custom tags
Let the user pick the entry version AND which tags to apply.

### 6. Save the entry

**If using Day One:**
Create the entry in the configured Learned journal with:
- The chosen version as the entry text
- If "Both" was selected, format as:
  ```
  [Refined version text]

  ---

  **As written:** [Original version text]
  ```
- Corrected tags (use the matched existing tags when there were typos)
- Current date/time

**If using markdown:**
Append to the configured markdown file:
```markdown
---

**Date:** YYYY-MM-DD HH:MM
**Tags:** #tag1 #tag2

[Entry text]
```

### 7. Confirm

Confirm with a brief message showing what was logged (and where).

If no arguments provided, ask the user what they learned.
