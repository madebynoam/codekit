---
name: dev:pr-respond
description: Draft a response to a PR comment or review with full context
arguments:
  - name: url
    description: GitHub PR URL or number
    required: true
---

Draft a thoughtful response to a PR comment or review.

## Instructions

### 1. Fetch PR context
- Get the PR title, description, and recent commits
- Fetch all comments and reviews
- Identify who commented and what they said

### 2. Understand the feedback
- Summarize the key points raised
- Identify what needs to be addressed
- Note any questions that were asked

### 3. Check what's been done
- Look at recent commits on the branch
- See if the feedback has already been addressed
- Identify any remaining work

### 4. Draft the response
Format the response for GitHub:
- Address the reviewer by @username
- Thank them for the feedback
- Explain what was done to address each point
- Use bullet points or lists for clarity
- Include tables if comparing before/after or listing multiple items
- Mention any follow-up items or things left for later
- Keep it concise but complete

### 5. Handle formatting
- GitHub supports markdown tables, but add blank line before them
- If tables render poorly, offer a list alternative
- Ask if user wants to include screenshots (provide placeholder)

### 6. Present for review
- Show the drafted response
- Ask if user wants any changes
- Offer to post it directly or let user copy/paste

## Example Response Structure

```markdown
Hey @reviewer, thanks for the feedback!

**[Topic 1]** - [What was done]
- Detail 1
- Detail 2

**[Topic 2]** - [What was done]

[Optional table or list]

Let me know if this looks good!
```

PR URL/number: $ARGUMENTS
