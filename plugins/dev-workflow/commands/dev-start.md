---
name: dev:start
description: Universal start command - auto-detects project type and starts dev server
---

# Start Development Server

**Universal command** - Works in ANY repository. Automatically detects your project type and starts the dev server.

## Instructions for Claude Code

**CRITICAL: Follow these steps in order. Do NOT skip the port conflict check.**

### Step 1: Detect Project Type
Check for these in order:
1. `package.json` with scripts: `start-a8c-for-agencies`, `start`, `dev`, `develop`, `serve`
2. `Makefile` with targets: `start`, `run`, `serve`
3. `docker-compose.yml`
4. Framework-specific files: `next.config.js`, `vite.config.js`, `Gemfile`, `manage.py`

### Step 2: Check Node.js Version (if Node.js project)
1. Read `package.json` engines field
2. Check current Node version with `node --version`
3. If versions don't match and nvm is available:
   - Run `nvm install <required-version>`
   - Run `nvm use <required-version>`

### Step 3: Check for Port Conflicts **BEFORE KILLING ANYTHING**

**MANDATORY: You MUST check if the port is in use BEFORE attempting to start the server.**

1. Determine the default port for this project (usually 3000 for Node.js projects)
2. Run `lsof -i :<port>` to check if port is in use
3. **IF port is in use:**
   - Show the user what's using it (PID, command, path)
   - **STOP and ASK the user** what they want to do:
     - Option 1: Kill the existing process and start here
     - Option 2: Use a different port (suggest next available port)
   - **WAIT for user response**
   - Only proceed after user chooses an option
4. **IF port is free:**
   - Proceed directly to Step 4

**DO NOT automatically kill processes without asking first!**

### Step 4: Start the Server
1. Run the detected command in background with `run_in_background: true`
2. Show startup output
3. Display the URL when server is ready

## Usage

```bash
/start
```

## What This Does

Detects your project type and runs the appropriate start command automatically.

## Auto-Detection Steps

The command checks for these in order:

### 1. package.json Scripts (Node.js projects)
Looks for these scripts in this order:
- `start-a8c-for-agencies` (wp-calypso A4A)
- `start` (most common)
- `dev` (Vite, Next.js, etc.)
- `develop` (Gatsby, etc.)
- `serve` (some projects)

### 2. Makefile (Make-based projects)
```bash
make start  # or make run, make serve
```

### 3. docker-compose.yml (Docker projects)
```bash
docker-compose up
```

### 4. Common Framework Patterns
- **Next.js**: Detects `next.config.js` → runs `npm run dev`
- **Vite**: Detects `vite.config.js` → runs `npm run dev`
- **Rails**: Detects `Gemfile` → runs `rails server`
- **Django**: Detects `manage.py` → runs `python manage.py runserver`
- **Flask**: Detects Flask app → runs `flask run`

## Auto-Fix Features

The command automatically handles common environment issues:

### Node.js Version Management
- Reads `package.json` engines field to detect required Node version
- Automatically installs correct version via nvm if available
- Switches to the correct version before starting
- Example: If project needs Node v22.9.0 but you have v20.x, it will:
  1. Run `nvm install 22.9.0`
  2. Run `nvm use 22.9.0`
  3. Start the server

### Dependency Checks
- Verifies package manager (npm/yarn/pnpm)
- Can auto-install dependencies if missing (asks first for large installs)

### Port Conflicts
- Detects if default port is in use
- Asks user whether to kill existing process or use alternative port
- Provides process information (PID, command) for informed decision

## Process

1. **Detect project type** - Check package.json, Makefile, docker-compose, etc.
2. **Auto-fix environment** - Install correct Node.js version via nvm if needed
3. **Start server** - Automatically run the detected command in background
4. **Show output** - Display server logs and URL

## Example: wp-calypso (A4A)

```
Detected: Node.js project (yarn)
Found script: start-a8c-for-agencies
Running: yarn start-a8c-for-agencies

[server] Building packages...
[server] Server listening on http://localhost:3000
[server] Webpack compiled successfully

✓ Development server started at http://localhost:3000
```

## Example: Next.js Project

```
Detected: Next.js project (npm)
Found script: dev
Running: npm run dev

ready - started server on 0.0.0.0:3000
✓ Development server started at http://localhost:3000
```

## Example: Rails Project

```
Detected: Ruby on Rails project
Running: rails server

=> Booting Puma
=> Rails 7.0.0 application starting in development
=> Run `bin/rails server --help` for more startup options
Puma starting in single mode...
* Listening on http://localhost:3000

✓ Development server started at http://localhost:3000
```

## After Starting

The server runs in the background:
- Visit the URL shown in output
- Make code changes (hot-reload if supported)
- Use `/stop` to stop it when done
- Continue working in your IDE

## If It Can't Detect

If the command can't auto-detect your project:

```
Could not auto-detect project type.
Please tell me how to start your development server:
```

Just tell Claude what command to run, and it will remember for next time.

## Port Conflicts

If the port is already in use, you'll be asked to choose:

```
⚠️  Port 3000 is already in use by:
    PID 12345: node /path/to/project/server.js

What would you like to do?
1. Kill the existing process and start here
2. Use a different port (e.g., 3001)

Choose option (1 or 2):
```

**Option 1: Kill existing process**
- Stops the conflicting process
- Starts the server on the intended port
- Useful when the old process is from the same project

**Option 2: Use different port**
- Starts the server on the next available port
- Keeps the existing process running
- Useful when both servers need to run simultaneously

You can also manually manage processes:
```bash
/stop           # Stop existing server
/start          # Try again
```

## Troubleshooting

**Server won't start:**
1. Check the error message
2. Try `/stop` first
3. Run `/build` if needed
4. Check project-specific requirements

**Wrong command detected:**
Tell Claude the correct command and it will use that next time.

## Notes

- **Mostly automatic** - Detects and fixes issues, prompts only when needed (port conflicts)
- **Runs in background** - You can keep working while server starts
- **Smart detection** - Checks multiple indicators and environment requirements
- **Portable** - Works in any project with zero configuration
- **Self-healing** - Auto-installs Node versions, intelligently handles port conflicts

## Project-Specific Details

### wp-calypso A4A
- Runs: `yarn start-a8c-for-agencies`
- Port: 3000
- Node: v22.9.0+ (auto-installed via nvm)
- Hot reload: Yes
- Build on start: Yes
- First build: ~2-5 minutes

### Common Ports
- 3000 - Most Node.js projects, Rails
- 8000 - Django
- 5000 - Flask
- 4200 - Angular
- 8080 - Vue CLI, Spring Boot

---

**This command works everywhere! Copy `.claude/commands/` to any project and `/start` will just work.**
