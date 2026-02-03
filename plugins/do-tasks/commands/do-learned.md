# Learned - Quick Journal Entry

Log something you learned to your Day One "Learned" journal.

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

1. Extract the main message (everything before any hashtags)
2. Extract all tags if present (words after #, without the # symbol)

3. **Smart tag matching and suggestion**:
   - First, query recent entries from the Learned journal to get a list of existing tags
   - **If user provided tags**: check if they closely match existing tags (typo detection). If a tag looks like a typo (e.g., "ai-ny" instead of "ai-nyc"), suggest the correct one
   - **If user provided NO tags**: analyze the content and suggest 2-4 relevant tags from the existing tag list. Include these suggested tags in the AskUserQuestion step so the user can select which ones to apply (or skip all)

4. Generate TWO versions of the entry:
   - **Original**: The message exactly as the user typed it
   - **Refined**: A cleaner, more complete version that:
     - Fixes typos and grammar
     - Adds context that would help with future recall
     - Makes it self-contained (would make sense if you read it months later)
     - Keeps it concise (1-3 sentences max)

5. Use AskUserQuestion to present options:
   - **Question 1 (Entry version)**:
     - Option 1: The refined version (recommended)
     - Option 2: The original text (as written)
     - Option 3: Both versions together
   - **Question 2 (Tags)** - always include this question as multi-select:
     - Show the top 3 most relevant existing tags based on content, ordered by relevance
     - Add "Skip tags" as the 4th option
     - User can select multiple tags, or choose "Other" to type custom tags
   Let the user pick the entry version AND which tags to apply.

6. Create the entry in the "Learned" journal with:
   - The chosen version as the entry text
   - If "Both" was selected, format as:
     ```
     [Refined version text]

     ---

     **As written:** [Original version text]
     ```
   - Corrected tags (use the matched existing tags when there were typos)
   - Current date/time

7. Confirm with a brief message showing what was logged.

If no arguments provided, ask the user what they learned.
