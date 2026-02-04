# Stop Development Server

**Universal command** - Works in ANY repository. Automatically stops the running development server.

## Usage

```bash
/stop
```

## What This Does

Finds and stops the running development server using multiple detection methods.

## Detection Methods

Tries these approaches in order:

### 1. Find Process by Common Ports
```bash
# Check these common dev server ports:
- 3000 (Node.js, Rails, Next.js, Create React App)
- 8000 (Django)
- 5000 (Flask)
- 4200 (Angular)
- 8080 (Vue CLI, Spring Boot)
- 5173 (Vite)
```

### 2. Find by Process Name
```bash
# Search for common dev server processes:
- node (Node.js servers)
- rails (Rails server)
- python (Django/Flask)
- webpack-dev-server
- vite
- next-server
```

### 3. Check docker-compose
```bash
# If project uses Docker:
docker-compose down
```

## Process

1. **Detect** - Find the running server
2. **Confirm** - "Found server on port 3000. Stop it?"
3. **Stop gracefully** - Send SIGTERM first
4. **Force if needed** - Send SIGKILL if it doesn't stop
5. **Verify** - Confirm it's stopped

## Example Output

```
Searching for running development server...

Found process:
  PID: 12345
  Port: 3000
  Command: node build/server.js

Stopping server gracefully...
✓ Server stopped successfully
```

---

**This command works everywhere! It automatically detects and stops whatever dev server you're running.**
