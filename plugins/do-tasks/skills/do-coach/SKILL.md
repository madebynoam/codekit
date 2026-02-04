---
name: do-coach
description: Prioritization coach that helps decide what to work on next through quick questions about impact, urgency, and effort. Considers long-term goals and maintains session history. Triggers on "/do:coach", "/do:what", "/do:next", or "what should I work on", "help me prioritize".
---

# Prioritization Coach

A quick coaching session to help pick the right task to work on.

## Persistent Files

**Goals** (`~/.claude/goals.md`): Long-term aspirations and priorities. Read at start of each session.

**History** (`~/.claude/coach-history.md`): Session log for continuity. Append after each session.

### Goals File Format

```markdown
# Goals & Aspirations

## Career
- Grow into a senior role
- Build portfolio pieces that demonstrate impact

## Personal
- Learn a new skill outside of work
- More time for creative projects

## Current Focus (this quarter)
- Ship current project improvements
- Establish repeatable patterns
```

If no goals file exists, offer to set them up. **Ask one question at a time** — don't overwhelm with multiple questions. Flow:
1. "What are you working toward in your career?" → wait for answer
2. "What matters to you personally outside work?" → wait for answer
3. "What's your focus this quarter?" → wait for answer
Then create the file.

### History File Format

```markdown
# Coach History

## 2026-01-29

**Tasks reviewed:** 10
**Recommended:** Work on onboarding flow
**Chose:** Side project prototype
**Reason:** Needed a warmup
**Aligned with goal:** Learn a new skill

---
```

## Modes

**Quick mode** (default): 2-minute check-in. Scan tasks, ask 1-2 pointed questions, recommend one task.

**Deep mode** (`--deep`): Thorough review with goal alignment scoring.

## Session Flow

### 1. Load Context

Read in order:
1. `~/.claude/goals.md` — understand what matters long-term
2. `~/.claude/coach-history.md` — check recent patterns
3. `~/.claude/user-tasks.md` — global tasks
4. `.claude/tasks.md` — project tasks (if exists)

Note from history:
- Tasks that keep getting deferred (flag for discussion)
- What was recommended vs chosen last time
- Goal alignment patterns

### 2. List Tasks with Goal Tags

Show tasks with goal alignment hints:

```
Tasks (10 pending):

1. Dashboard redesign
2. Fix landing page responsiveness
3. Onboarding flow updates [Career: project]
4. Write blog post about workflow [Career: portfolio]
5. Side project prototype [Personal: new skill]
...
```

### 3. Offer Context Lookup

> Want me to check Slack/Linear/P2 for context? (y/n)

If yes: Use `context-a8c` provider for relevant threads.

### 4. Quick Triage

Assess each task on:
- **Impact**: Does this move something meaningful forward?
- **Urgency**: Real deadline or external dependency?
- **Effort**: Quick win or deep work?
- **Goal alignment**: Does this serve a long-term aspiration?

Ask about 1-2 tasks:

> "Side project" keeps getting deferred. Is this actually a priority, or should we drop it from the list?

> "Write blog post" — this aligns with your portfolio goal. When's the right time?

### 5. Challenge Assumptions

General calibration:
- Async work means no one expects instant responses
- "ASAP" often means "whenever"
- Perfectionism on low-visibility work is wasted

Goal-based challenges:
> This task doesn't align with any of your stated goals. Is it actually important, or just urgent-feeling?

> You've deferred [goal-aligned task] 3 times. What's blocking you?

### 6. Recommend

```
Recommendation: Work on [task]

Why: [1 sentence — impact, timing, or goal alignment]

Goal alignment: [which goal this serves]

Defer: [tasks that can wait]
Quick-pass: [tasks that don't need perfection]
Drop candidate: [tasks that don't serve any goal]
```

### 7. Log Session

After user confirms choice, append to `~/.claude/coach-history.md`:

```markdown
## [date]

**Tasks reviewed:** [count]
**Recommended:** [task]
**Chose:** [what user picked]
**Reason:** [if different from recommendation]
**Aligned with goal:** [goal or "none"]
```

## Deep Mode (`--deep`)

Full review with goal scoring:

| Task | Impact | Urgency | Effort | Goal | Verdict |
|------|--------|---------|--------|------|---------|
| Onboarding flow | High | Medium | 2hr | Career | **Do today** |
| Side project | Medium | Low | 1hr | Personal | Schedule |
| Fix landing page | Medium | Low | 1hr | None | Quick-pass |

## Pattern Insights

After 5+ sessions, offer insights:

> You tend to defer personal goals for work tasks. Want to protect time for your side project?

> "Write blog post" has been on your list for 2 weeks. Either schedule it or drop it.

## Quick Reference

**Eisenhower + Goals:**
- Urgent + Important + Goal-aligned → Do now
- Important + Goal-aligned, not urgent → Schedule it
- Urgent, not important, no goal → Delegate or quick-pass
- No urgency, no importance, no goal → Drop it

**Red flags:**
- "I should probably..." (guilt, not priority)
- "It's been on my list forever" (sunk cost)
- "Someone might notice" (they probably won't)
- Task doesn't serve any stated goal (why is it here?)
