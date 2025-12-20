# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine-tools/cli` is the custom monorepo CLI tool that powers `yarn affine` (or `yarn af`) commands.

## Usage

```bash
yarn affine -h              # Show help
yarn affine <pkg> <script>  # Run package script
yarn af web dev             # Shorthand

# Common commands
yarn affine init            # Generate monorepo files
yarn affine clean --dist    # Clean dist folders
yarn affine clean --node-modules  # Clean node_modules
yarn affine build           # Build packages
yarn affine dev             # Start dev servers

# Package-specific
yarn affine @affine/native build
yarn affine @affine/server dev
yarn affine @affine/electron make
```

## Architecture

### Entry Point

- `bin/cli.js` - CLI entry
- `bin/runner.js` - Script runner with ts-node
- `src/affine.ts` - Main CLI definition using Clipanion

### Commands (`src/`)

- `run.ts` - Run package scripts
- `dev.ts` - Start dev servers
- `build.ts` - Build packages (webpack)
- `bundle.ts` - Bundle for production
- `init.ts` - Initialize/generate files
- `clean.ts` - Clean artifacts
- `cert.ts` - Certificate management

### Key Features

**TypeScript Support**: The `r` binary (runner.js) auto-injects ts-node/swc transpilation, allowing direct execution of `.ts` files in package scripts.

**Package Resolution**: Uses `@affine-tools/utils/workspace` to resolve workspace packages by name.

**Webpack Integration**: Build and dev commands use webpack with custom configuration for the monorepo structure.

## Development

To run a `.ts` script without explicit ts-node setup, packages can use `r`:

```json
{
  "scripts": {
    "dev": "r ./src/index.ts"
  }
}
```
