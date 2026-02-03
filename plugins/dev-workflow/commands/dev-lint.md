# Lint Code

**Universal command** - Works in ANY repository. Automatically detects and runs your linters.

## Usage

```bash
# Lint everything
/lint

# Lint specific file
/lint path/to/file.ts

# Lint and auto-fix
/lint --fix

# Lint specific file and fix
/lint --fix path/to/file.ts
```

## What This Does

Auto-detects your linters and runs them appropriately.

## Detection Logic

Checks for these in order:

### 1. package.json Scripts (Node.js)
Looks for these lint scripts:
- `lint`
- `lint:js`
- `eslint`
- `prettier`

### 2. Linter Configuration Files
- **ESLint**: `.eslintrc.js`, `.eslintrc.json`, or in package.json
- **Prettier**: `.prettierrc`, `prettier.config.js`
- **Stylelint**: `.stylelintrc` (for CSS/SCSS)
- **TSLint**: `tslint.json` (legacy)

### 3. Language-Specific Linters
- **Python**: `pylint`, `flake8`, `black`, `ruff`
- **Ruby**: `rubocop`
- **Go**: `golint`, `go vet`
- **Rust**: `cargo clippy`
- **PHP**: `phpcs`, `php-cs-fixer`

## Auto-Fix

Many linters support auto-fix:

```bash
/lint --fix
```

This runs:
- **ESLint**: `eslint --fix`
- **Prettier**: `prettier --write`
- **Rubocop**: `rubocop -a`
- **Black**: `black .` (auto-formats by default)
- **Rust fmt**: `cargo fmt`
- **Go fmt**: `gofmt -w`

## Specific Files

Lint a specific file:

```bash
/lint client/components/Button.tsx
```

The command figures out which linters apply to that file:
- `.tsx` → ESLint, Prettier
- `.py` → Pylint, Black
- `.rb` → Rubocop
- `.rs` → Clippy

## Multiple Linters

If multiple linters are detected, runs all of them:

```
Detected: ESLint, Prettier, Stylelint
Running all linters...

ESLint passed
Prettier passed
Stylelint passed
```

---

**This command works everywhere! It detects your linting setup and runs the appropriate linters.**
