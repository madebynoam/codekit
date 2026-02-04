---
name: dev:lint
description: Universal lint command - auto-detects and runs your linters
---

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

## Example: wp-calypso (ESLint)

```
Detected: ESLint (yarn)
Running: yarn lint:js

✓ All files pass linting

Or with issues:
client/components/Button.tsx
  23:5  error  'React' must be in scope  react/react-in-jsx-scope
  
✖ 1 problem (1 error, 0 warnings)
  Potentially fixable with --fix option
```

## Example: Python (Black + Flake8)

```
Detected: black, flake8
Running: black . && flake8

All done! ✨
12 files left unchanged.

Or with issues:
app/models.py:45:80: E501 line too long (88 > 79 characters)
```

## Example: Rust (Clippy)

```
Detected: Cargo with clippy
Running: cargo clippy

warning: unused variable: `x`
  --> src/main.rs:10:9

warning: 1 warning emitted
```

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

## Common Issues & Auto-Fixes

The command will auto-fix these when using `--fix`:
- Missing semicolons
- Incorrect indentation
- Trailing whitespace
- Import order
- Quote style
- Spacing issues

## Pre-commit Integration

If the project has pre-commit hooks, the command respects them:

```
Detected: pre-commit hooks
Running linters configured in .pre-commit-config.yaml
```

## Multiple Linters

If multiple linters are detected, runs all of them:

```
Detected: ESLint, Prettier, Stylelint
Running all linters...

✓ ESLint passed
✓ Prettier passed  
✓ Stylelint passed
```

---

**This command works everywhere! It detects your linting setup and runs the appropriate linters.**
