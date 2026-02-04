---
name: dev:branch
description: Pull latest trunk and create a new branch with a properly formatted name
arguments:
  - name: intent
    description: What you're working on (e.g., "fix: slider always showing as full")
    required: true
---

Create a new feature branch from the latest trunk with a properly formatted name.

## Branch Naming Conventions

This repo uses these prefixes:
- `add/` - New features or functionality
- `update/` - Enhancements to existing features
- `fix/` - Bug fixes
- `try/` - Experiments or exploratory work

Branch names should be kebab-case, concise, and descriptive.

## Instructions

### 1. Parse the intent
Analyze: `$ARGUMENTS`

Determine:
- **Type**: Is this a fix, new feature, update, or experiment?
- **Scope**: What component/area is affected?
- **Description**: What's the core change?

### 2. Validate or clarify
If the intent is ambiguous, ask for clarification. Examples of when to ask:
- "improve performance" → Which area? What kind of improvement?
- "update thing" → Is this a bug fix or enhancement?
- Single word like "slider" → What about the slider?

If clear, proceed.

### 3. Generate branch name
Format: `{prefix}/{concise-kebab-description}`

Rules:
- Use lowercase kebab-case
- Keep it under 50 chars if possible
- Be specific but concise
- Include component name if relevant (e.g., `fix/a4a-slider-overflow`)
- If there's a ticket number, use format: `{prefix}/{TICKET-123}/description`

### 4. Show proposed branch and confirm
Display:
```
Intent: {original intent}
Branch: {proposed-branch-name}
```

Ask user to confirm or suggest alternative.

### 5. Pull latest trunk
```bash
git checkout trunk
git pull origin trunk
```

### 6. Create and checkout new branch
```bash
git checkout -b {branch-name}
```

### 7. Report success
Show:
- ✓ Pulled latest trunk
- ✓ Created branch: `{branch-name}`
- Ready to start work!

## Examples

| Intent | Branch Name |
|--------|-------------|
| "fix: slider always showing as full" | `fix/slider-always-full` |
| "add dark mode toggle" | `add/dark-mode-toggle` |
| "update login flow to use oauth" | `update/login-oauth-flow` |
| "try using redis for caching" | `try/redis-caching` |
| "a4a: fix responsive breakpoint" | `fix/a4a-responsive-breakpoint` |
| "DOTCOM-1234: fix header alignment" | `fix/DOTCOM-1234/header-alignment` |
