# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

AFFiNE is a privacy-focused, local-first, open-source alternative to Notion & Miro. It combines docs, whiteboards, and databases into a single hyper-fused platform.

## Build Commands

The monorepo uses a custom CLI tool (`yarn affine` or `yarn af`). Node.js <23.0.0 required (see `.node-version` for exact version).

```bash
# Install dependencies (uses Yarn 4.x with corepack)
corepack enable
yarn install

# Build native dependencies (requires Rust toolchain)
yarn affine @affine/native build      # Frontend native modules
yarn affine @affine/server-native build  # Server native modules

# Development
yarn dev                 # Start web frontend dev server
yarn affine server dev   # Start backend server (requires Docker services)
yarn affine @affine/electron dev  # Start desktop app dev

# Build
yarn build               # Build web frontend
yarn affine @affine/electron build  # Build desktop app

# Code quality
yarn lint               # ESLint + Prettier
yarn lint:fix           # Fix lint issues
yarn typecheck          # TypeScript check
```

## Testing

```bash
# Unit tests (vitest)
yarn test                           # Run all unit tests
yarn test path/to/file.spec.ts      # Run specific test file

# E2E tests (Playwright)
npx playwright install              # First-time setup
yarn workspace @affine-test/affine-local e2e

# Server tests (ava)
yarn workspace @affine/server test
```

## Architecture

### Package Structure

- `packages/frontend/core` - Main web application (React 19, Jotai, react-router)
- `packages/frontend/component` - Reusable UI components
- `packages/frontend/apps/` - Platform-specific apps (web, electron, mobile, android, ios)
- `packages/frontend/native` - Native Rust modules (SQLite bindings via NAPI-RS)
- `packages/backend/server` - NestJS server with GraphQL API, Prisma ORM
- `packages/common/infra` - Core infrastructure (framework, LiveData, ORM, storage)
- `blocksuite/` - Collaborative editor framework (forked, integrated as monorepo)
- `tools/cli` - Custom monorepo CLI (`@affine-tools/cli`)
- `tests/` - E2E and integration tests (Playwright)

### Key Architectural Patterns

**Frontend Module System**: `packages/frontend/core/src/modules/` contains feature modules. Each module typically exports services, stores, and UI components. The DI container uses `@toeverything/infra` framework.

**LiveData**: Reactive state management pattern in `@toeverything/infra`. Wraps observables with `.value` accessor and `.subscribe()` for reactivity.

**BlockSuite Integration**: The editor (`blocksuite/`) provides block-based editing with CRDT sync (Yjs). AFFiNE extends it via blocks in `blocksuite/affine/blocks/`.

**Server Architecture**: NestJS with modules in `packages/backend/server/src/core/` (auth, workspaces, doc, sync, etc.). Uses GraphQL API with Prisma for database.

### Development Services (Docker)

For server development, start required services:
```bash
cp .docker/dev/compose.yml.example .docker/dev/compose.yml
cp .docker/dev/.env.example .docker/dev/.env
docker compose -f .docker/dev/compose.yml up
```

Then initialize:
```bash
cp packages/backend/server/.env.example packages/backend/server/.env
yarn affine server init
```

Test users: `dev@affine.pro/dev` (default), `pro@affine.pro/pro` (pro), `team@affine.pro/team` (team)

### Desktop Build Process

Building Electron app requires a two-phase yarn configuration due to hoisting limitations:
1. Build core with default yarn settings
2. Reinstall with `nmMode: classic` and `nmHoistingLimits: workspaces`
3. Run `yarn affine @affine/electron make`

See `docs/building-desktop-client-app.md` for details.
