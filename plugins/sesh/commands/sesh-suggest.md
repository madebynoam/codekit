---
name: sesh:suggest
description: Analyze current session and suggest reusable commands
arguments: []
---

Analyze the current session and suggest what workflows could become reusable commands.

## Instructions

### 1. Review session activities
Look at what was done in this session:
- What tasks were repeated or could be repeated?
- What multi-step workflows were performed?
- What required specific domain knowledge?

### 2. Identify command candidates
Good commands have these traits:
- **Repeatable**: Will be done again in future sessions
- **Multi-step**: More than just a single action
- **Generalizable**: Works across different contexts
- **Time-saving**: Automates tedious or error-prone steps

### 3. Categorize suggestions

**High value** - Complex workflows done frequently:
- Git workflows (branching, rebasing, merging)
- PR/code review flows
- Testing and validation patterns

**Medium value** - Useful but less frequent:
- Debug/testing toggles
- Environment setup
- Documentation generation

**Lower value** - Simple or rarely repeated:
- One-off investigations
- Context-specific fixes

### 4. Present suggestions

For each suggested command, provide:
- **Name**: Using existing namespace (e.g., `craft:command-name`)
- **Purpose**: What problem it solves
- **Trigger**: When would someone use it
- **Steps**: What it would automate

### 5. Ask which to create

Let user pick which commands to create, then help build them following the command file format:
```yaml
---
name: namespace:command-name
description: Short description
arguments:
  - name: arg-name
    description: What this arg does
    required: true/false
---

Command instructions here...
```

## Example Output

Based on this session, here are potential commands:

**High Value:**
1. `craft:responsive-button` - Apply responsive styling pattern to buttons
   - Trigger: When adding CTAs that need mobile/desktop sizing
   - Steps: Identify parent layout, choose align-self vs width approach, add breakpoint

**Medium Value:**
2. `craft:jtbd-copy` - Improve CTA copy using Jobs-to-be-Done principles
   - Trigger: When reviewing button/link text
   - Steps: Identify user goal, draft options, compare in table format

Which of these would you like me to create?
