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
Port 3000 is already in use by:
    PID 12345: node /path/to/project/server.js

What would you like to do?
1. Kill the existing process and start here
2. Use a different port (e.g., 3001)

Choose option (1 or 2):
```

## Common Ports
- 3000 - Most Node.js projects, Rails
- 8000 - Django
- 5000 - Flask
- 4200 - Angular
- 8080 - Vue CLI, Spring Boot

---

**This command works everywhere! It detects your project type and starts the dev server.**
