# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/web` is the web application entry point. It's a thin wrapper that bootstraps `@affine/core` for browser deployment.

## Commands

```bash
yarn dev      # Start dev server (from repo root)
yarn build    # Build for production
```

## Architecture

This package is intentionally minimal:
- Provides webpack/vite entry point
- Configures environment for web browsers
- Imports and mounts `@affine/core`

### Entry Point

```
src/
└── index.ts  # Web entry, imports @affine/core bootstrap
```

### Build Configuration

Build configuration is handled by the monorepo CLI (`yarn affine`). See `tools/cli/` for webpack configuration.

### Relationship to Core

All application logic lives in `@affine/core`. This package only handles:
- HTML template
- Web-specific environment setup
- Production build output

### Development

During development, the dev server serves this package with hot reload:
```bash
yarn dev  # Starts webpack-dev-server
```

Access at http://localhost:8080 (or configured port).
