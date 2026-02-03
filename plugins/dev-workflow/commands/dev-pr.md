---
name: dev:pr
description: Create a draft PR with proper structure - problem first, no AI attribution
arguments:
  - name: title
    description: PR title (optional - will be inferred from branch/commits if not provided)
    required: false
---

Create a well-structured draft PR.

## Key Principles

1. **Problem first** - Always explain WHY before WHAT
2. **No AI attribution** - Never add "Generated with Claude Code" or similar
3. **Draft by default** - PRs are created as drafts for review
4. **Checklist accuracy** - Only check items that actually apply

## Instructions

### 1. Gather context

Run in parallel:
- `git status` - Check for uncommitted changes
- `git log origin/trunk..HEAD --oneline` - See all commits to include
- `git diff origin/trunk...HEAD --stat` - See all files changed
- Check if branch tracks remote and needs pushing

If there are uncommitted changes, warn the user and ask if they want to commit first.

### 2. Analyze the changes

From the commits and diff, identify:
- **The problem being solved** - What was broken/missing/needed?
- **The solution approach** - How does this fix address it?
- **Files affected** - Which areas of the codebase?
- **Testing considerations** - What needs manual verification?

### 3. Determine PR title

If title provided: Use `$ARGUMENTS`

If not provided, infer from:
- Branch name (e.g., `fix/a4a-slider-overflow` → "A4A: Fix slider overflow")
- Commit messages
- Follow format: `{Area}: {Brief description}`

### 4. Draft the PR body

Follow this structure:

```markdown
## Proposed Changes

- {Bullet list of what changed}

## Why are these changes being made?

{Explain the problem that existed. What was broken? What user pain did this cause?
This is the MOST IMPORTANT section - future developers need to understand WHY.}

## Testing Instructions

{Step-by-step instructions to verify the fix}
- [ ] Navigate to {path}
- [ ] Do {action}
- [ ] Verify {expected result}
```

### 5. Show preview and confirm

Display the full PR content and ask user to confirm or edit.

### 6. Create the PR

```bash
# Push if needed
git push -u origin {branch-name}

# Create draft PR
gh pr create --draft --title "{title}" --body "{body}"
```

### 7. Report success

Show:
- PR URL
- Remind user it's a draft - mark ready when tests pass

## What NOT to include

- "Generated with Claude Code" or any AI attribution
- "Made with AI" or similar
- Emojis (unless user explicitly uses them)
- Overly verbose descriptions - be concise
- Checked items that don't apply to this PR

## Examples

### Good "Why" section:
```
The marketplace slider was displaying incorrectly - the progress
fill appeared always full or reversed, making it difficult for users
to understand their current selection state.
```

### Bad "Why" section:
```
This PR adds a fill area to the slider component.
```

(The bad example describes WHAT, not WHY)
