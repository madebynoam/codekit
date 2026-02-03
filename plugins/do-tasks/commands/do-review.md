# Learned Review - Show What You've Learned

Review entries from your Day One "Learned" journal.

## Usage
```
/learned-review [filter]
```

## Filters
- `today` - Show entries from today
- `yesterday` - Show entries from yesterday
- `week` - Show entries from the last 7 days
- `#tag` - Show entries with a specific tag (e.g., `#ai-nyc`)
- No filter - Show entries from today by default

## Examples
```
/learned-review today
/learned-review yesterday
/learned-review week
/learned-review #ai-nyc
```

## Instructions

Parse the filter from: $ARGUMENTS

1. Determine the filter type:
   - If empty or "today": query entries from today
   - If "yesterday": query entries from yesterday
   - If "week": query entries from the last 7 days
   - If starts with "#": search for entries with that tag

2. Query the "Learned" journal with appropriate date range or search query

3. Use AskUserQuestion to ask how they want to see the results:
   - **List view**: Show each entry as a bullet point with tags
   - **Summary**: Generate a synthesized summary that groups related learnings, highlights key themes, and presents insights in a digestible narrative format

4. Present based on their choice:

   **For List view**:
   - Group by date if showing multiple days
   - Show each entry as a clean bullet
   - Include tags inline
   - Show total count

   **For Summary**:
   - Group related learnings by theme/topic
   - Write a brief narrative synthesis
   - Highlight connections between entries
   - End with key takeaways
   - Keep it concise but insightful

5. If no entries found, let the user know in a friendly way.
