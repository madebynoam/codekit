# Build Project

**Universal command** - Works in ANY repository. Automatically detects and runs your build process.

## Usage

```bash
# Standard build
/build

# Build for production
/build --production

# Clean build
/build --clean
```

## What This Does

Auto-detects your build system and runs the appropriate build command.

## Detection Logic

Checks for these in order:

### 1. package.json Scripts (Node.js)
Looks for these build scripts:
- `build` (most common)
- `build:prod`
- `compile`
- `dist`

### 2. Build Tools
- **Webpack**: Detects `webpack.config.js`
- **Vite**: Detects `vite.config.js` → `vite build`
- **Rollup**: Detects `rollup.config.js`
- **esbuild**: Detects `esbuild.config.js`
- **tsc**: Detects `tsconfig.json` → `tsc`
- **Babel**: Detects `.babelrc`

### 3. Framework Build Commands
- **Next.js**: `next build`
- **Gatsby**: `gatsby build`
- **Create React App**: `npm run build`
- **Vue CLI**: `vue-cli-service build`
- **Angular**: `ng build`

### 4. Other Build Systems
- **Make**: Detects `Makefile` → `make build`
- **Gradle**: Detects `build.gradle` → `./gradlew build`
- **Maven**: Detects `pom.xml` → `mvn package`
- **Cargo**: Detects `Cargo.toml` → `cargo build`
- **Go**: Detects `go.mod` → `go build`

## Clean Build

Force a clean build (removes old build artifacts first):

```bash
/build --clean
```

The command detects the clean command:
- Node.js: `yarn clean && yarn build`
- Cargo: `cargo clean && cargo build`
- Make: `make clean && make build`

## Production Build

Build for production (optimized):

```bash
/build --production
```

Runs:
- Node.js: `NODE_ENV=production yarn build`
- Next.js: `next build` (already production)
- Cargo: `cargo build --release`

---

**This command works everywhere! It detects your build system and builds appropriately.**
