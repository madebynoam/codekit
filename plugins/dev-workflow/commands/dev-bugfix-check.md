---
name: dev:bugfix-check
description: Pre-bug-fix commit checklist - document, find similar issues, prevent recurrence
---

# Pre-Bug-Fix Commit Checklist

Before committing this bug fix, let's ensure we've done our due diligence. This command helps prevent future bugs and documents the fix properly.

## 1. Document the Bug

First, let me analyze the changes you've made and draft a clear commit message that explains:
- **What** the bug was (observable symptom)
- **Why** it happened (root cause)
- **How** it was fixed (the solution)

This makes `git log` a useful debugging resource for future developers.

## 2. Find Similar Issues

Search the codebase for similar patterns that might have the same bug:
- Look for the same anti-pattern elsewhere
- Check if this is a copy-paste bug that exists in multiple places
- Identify any related code that should be updated together

## 3. Prevent Recurrence

Suggest concrete prevention measures:
- **Tests**: Write a test that would have caught this bug
- **Types**: Add TypeScript types that would prevent this at compile time
- **Linting**: Suggest ESLint rules that could catch this pattern
- **Runtime checks**: Add assertions or validations if appropriate

## 4. Understand the Pattern

Identify the larger class of problems:
- What category does this bug fall into? (race condition, off-by-one, null reference, stale closure, etc.)
- Are there architectural changes that would eliminate this class of bugs?
- Should this be added to the project's CLAUDE.md or coding guidelines?

---

## Instructions

Please analyze my current staged changes (or recent changes if nothing is staged) and walk me through this checklist. Be thorough but concise.

Start by running `git diff --cached` (or `git diff` if nothing staged) to see what I'm about to commit.
