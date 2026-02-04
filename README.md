# codekit

Claude Code plugins for getting things done — task management, session continuity, universal dev commands, and component finding.

By [Noam Almosnino](https://noamalmos.com)

## Quick Start

In Claude Code, run:

```bash
# Add the marketplace
/plugin marketplace add madebynoam/codekit

# Install what you need
/plugin install do@codekit
/plugin install sesh@codekit
/plugin install dev-workflow@codekit
/plugin install find-component@codekit
```

## Plugins

### do — Task Management

A task stack with prioritization coaching. Add tasks, check them off, and get help deciding what to work on next.

| Command | What it does |
|---------|-------------|
| `/do:add fix the header` | Add a task (use `--local` for project-level) |
| `/do:add task 1 \| task 2` | Add multiple tasks at once |
| `/do:list` | Show all pending tasks |
| `/do:done 3` | Mark task #3 complete |
| `/do:done fix header` | Mark by text match |
| `/do:coach` | Quick prioritization check-in |
| `/do:coach --deep` | Thorough review with goal scoring |
| `/do:learned git rebase -i #git` | Log a learning to Day One |
| `/do:review week` | Review recent learnings |
| `/do:decompose the problem` | Break down a complex problem |
| `/do:refine-prompt my rough prompt` | Improve a prompt using Transformer principles |

The coach reads your `~/.claude/goals.md` and tracks decisions in `~/.claude/coach-history.md` to spot patterns over time.

### sesh — Session Continuity

Save sessions, pick up where you left off, and reflect on what you learned.

| Command | What it does |
|---------|-------------|
| `/sesh:save my-feature` | Save transcript + summary to `~/Claude Sessions/` |
| `/sesh:resume` | Read project context and show where you left off |
| `/sesh:reflect` | Guided reflection → Day One journal entry |
| `/sesh:close` | Save state, update trackers, show next steps |
| `/sesh:suggest` | Analyze session for reusable command ideas |

Sessions are saved to `~/Claude Sessions/{date}-{name}/` with both a human-readable summary and the raw transcript.

### dev-workflow — Universal Dev Commands

Auto-detecting commands that work in any repository. No configuration needed — they figure out your project type and do the right thing.

| Command | What it does |
|---------|-------------|
| `/dev:start` | Start dev server (detects Next.js, Vite, Rails, Django, etc.) |
| `/dev:stop` | Stop running dev server |
| `/dev:build` | Build project (`--clean`, `--production`) |
| `/dev:lint` | Run linters (`--fix` for auto-fix) |
| `/dev:test` | Run tests (`--watch`, `--coverage`) |
| `/dev:commit` | Smart commit — groups changes logically, writes clear messages |
| `/dev:branch "fix: slider bug"` | Create properly named branch from trunk |
| `/dev:rebase` | Safely rebase with trunk (handles stash, conflicts, push) |
| `/dev:pr` | Create draft PR (problem-first, no AI attribution) |
| `/dev:pr-respond #123` | Draft response to PR review comments |
| `/dev:worktrees` | List git worktrees and branch status |
| `/dev:bugfix-check` | Pre-commit checklist for bug fixes |

**Supported project types**: Node.js, Python, Ruby, Go, Rust, PHP, Java, and anything with a `Makefile` or `docker-compose.yml`.

### find-component — Component Detective

Find where UI components live in a codebase from screenshots, routes, or names.

| Command | What it does |
|---------|-------------|
| `/find ~/Desktop/screenshot.png` | Find code from a screenshot |
| `/find settings/profile` | Find components for a route |
| `/find UserCard` | Find component definition and usage |

Works with React, Vue, Angular, and other component-based frameworks. Returns the main component file, styles, types, tests, hooks, sub-components, and Storybook stories.

## Installation

### Via Plugin Marketplace (Recommended)

```bash
/plugin marketplace add madebynoam/codekit
```

Then install individual plugins — you don't have to install everything:

```bash
/plugin install dev-workflow@codekit    # Just the dev commands
/plugin install do@codekit        # Just task management
```

### Manual

```bash
git clone https://github.com/madebynoam/codekit.git
cp -r codekit/plugins/dev-workflow/commands/* ~/.claude/commands/
cp -r codekit/plugins/do/skills/* ~/.claude/skills/
cp -r codekit/plugins/do/commands/* ~/.claude/commands/
# etc.
```

## Optional Dependencies

- **Day One** — `do:learned`, `do:review`, and `sesh:reflect` write to a Day One journal via MCP. These commands still work without Day One — they'll just skip the journaling part.
- **GitHub CLI** (`gh`) — `dev:pr` and `dev:pr-respond` use `gh` to create PRs and fetch comments.

## Philosophy

These started as personal tools built from real daily work — navigating large codebases, keeping track of tasks across sessions, and avoiding the "where was I?" problem every morning.

Three principles:

1. **Auto-detect everything** — Commands figure out your project type. No config files.
2. **Session continuity** — Work should survive closing the terminal.
3. **Coach, don't just track** — The task system doesn't just list tasks, it helps you pick the right one.

## Also See

- [dcode](https://github.com/madebynoam/dcode) — Design-focused Claude Code skills (UX copy improvement, pattern mining, session reflection for designers)

## License

MIT
