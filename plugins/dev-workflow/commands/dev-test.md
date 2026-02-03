# Run Tests

**Universal command** - Works in ANY repository. Automatically detects and runs your tests.

## Usage

```bash
# Run all tests
/test

# Run specific file
/test path/to/test-file.test.ts

# Run in watch mode
/test --watch
```

## What This Does

Auto-detects your testing framework and runs the appropriate test command.

## Detection Logic

Checks for these in order:

### 1. package.json Scripts (Node.js)
Looks for these test scripts:
- `test` (most common)
- `test:unit`
- `test:all`
- `jest`
- `vitest`
- `mocha`

### 2. Testing Frameworks
- **Jest**: Detects `jest.config.js` or in package.json
- **Vitest**: Detects `vitest.config.js`
- **Mocha**: Detects `.mocharc` or `test/mocha.opts`
- **Pytest**: Detects `pytest.ini` or `setup.py`
- **RSpec**: Detects `.rspec` or `spec/` directory
- **PHPUnit**: Detects `phpunit.xml`
- **Go**: Detects `*_test.go` files

### 3. Framework Commands
- **Node.js**: `npm test` or `yarn test`
- **Python**: `pytest` or `python -m pytest`
- **Ruby**: `rspec` or `bundle exec rspec`
- **Go**: `go test ./...`
- **PHP**: `phpunit`
- **Rust**: `cargo test`

## Watch Mode

Most frameworks support watch mode:

```bash
/test --watch
```

The command detects and runs:
- Jest: `yarn test --watch`
- Vitest: `yarn vitest --watch`
- Pytest: `pytest --watch` (via pytest-watch)

## Specific Files

Test a specific file:

```bash
/test client/components/Button.test.tsx
```

The command figures out the right way to run it.

## Coverage

Generate coverage report:

```bash
/test --coverage
```

---

**This command works everywhere! It detects your testing setup and runs tests appropriately.**
