# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/core` is the main web application for AFFiNE. It contains all feature modules, UI components, and business logic for the web/desktop/mobile frontends.

## Commands

```bash
yarn dev              # Start dev server (from repo root)
yarn test             # Run unit tests
```

## Architecture

### Module System

The application uses a custom DI framework from `@toeverything/infra`. Each feature lives in `src/modules/` and follows this pattern:

```
src/modules/<feature>/
├── index.ts           # Exports + configureXxxModule(framework)
├── entities/          # Entity classes (stateful objects with lifecycle)
├── services/          # Service classes (business logic, singleton per scope)
├── stores/            # Store classes (data access layer)
├── scopes/            # Scope definitions (DI container boundaries)
├── providers/         # Abstract interfaces for implementations
├── views/             # React components
└── events.ts          # Framework events
```

### Key Patterns

**Module Registration**: Each module exports a `configure*Module(framework)` function that registers entities, services, stores with the DI framework:

```typescript
framework
  .scope(WorkspaceScope)
  .service(DocsService, [DocsStore, DocPropertiesStore])
  .entity(Doc, [DocScope, DocsStore, WorkspaceService])
```

**Scopes**: Define DI container boundaries. Common scopes:
- Root scope (global singletons)
- `WorkspaceScope` - per-workspace instances
- `DocScope` - per-document instances

**LiveData**: Reactive state containers from `@toeverything/infra`. Use `.value` for current value, `.subscribe()` for changes, `useLiveData()` hook in React.

**Services vs Entities**: Services are singletons within their scope. Entities are created per-instance (e.g., one `Doc` entity per document).

### Directory Structure

- `src/bootstrap/` - App initialization, polyfills, platform detection
- `src/modules/` - Feature modules (67+ modules)
- `src/components/` - Shared React components
- `src/desktop/` - Desktop-specific (Electron) code
- `src/mobile/` - Mobile-specific code
- `src/commands/` - Command palette commands
- `src/utils/` - Utility functions

### Key Modules

- `workspace` - Workspace management, storage, sync
- `doc` - Document management
- `editor` - BlockSuite editor integration
- `cloud` - Cloud sync, auth, server communication
- `storage` - Local storage (IndexedDB, SQLite)
- `dialogs` - Modal dialogs system
- `workbench` - Main app layout, tabs, navigation

### BlockSuite Integration

The editor uses BlockSuite (`@blocksuite/*` packages). Integration points:
- `src/modules/editor/` - Editor service and components
- `src/blocksuite/` - BlockSuite extensions and customizations
