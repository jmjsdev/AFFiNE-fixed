# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@toeverything/infra` is the core infrastructure library providing the DI framework, reactive state management, storage abstractions, and other foundational utilities.

## Package Exports

```typescript
import { Framework, Service, Entity, Scope } from '@toeverything/infra';
import { LiveData, useLiveData } from '@toeverything/infra';
import { createORMClient, t, f } from '@toeverything/infra/orm';
```

## Architecture

### Framework (`src/framework/`)

Custom dependency injection framework with scoped containers:

**Core Concepts**:
- `Framework` - Root container builder
- `Service` - Base class for singleton services
- `Entity` - Base class for per-instance objects
- `Store` - Base class for data access layer
- `Scope` - Defines DI container boundaries
- `createIdentifier()` - Creates typed DI tokens

**Usage**:
```typescript
// Define a scope
const WorkspaceScope = Scope('workspace');

// Register services
framework
  .scope(WorkspaceScope)
  .service(DocsService, [DocsStore])
  .entity(Doc, [DocScope, DocsStore]);

// Create scoped container
const workspaceContainer = framework.provider.scope(WorkspaceScope).get(WorkspaceService);
```

### LiveData (`src/livedata/`)

Reactive state containers wrapping RxJS observables:

```typescript
const count$ = new LiveData(0);

// Read current value
count$.value;

// Subscribe to changes
count$.subscribe(val => console.log(val));

// In React
const count = useLiveData(count$);

// Derive new LiveData
const doubled$ = count$.map(c => c * 2);
```

**Operators**: `mapInto`, `catchErrorInto`, `exhaustMapSwitchUntilChanged`, `backoffRetry`, `smartRetry`

### ORM (`src/orm/`)

Lightweight ORM for Yjs documents:

```typescript
const client = createORMClient({
  tables: {
    docs: t.table({
      id: t.string().primaryKey(),
      title: f.string(),
      createdAt: f.number(),
    }),
  },
});
```

### Storage (`src/storage/`)

Abstractions for persistent storage (IndexedDB, SQLite, memory).

### Atom (`src/atom/`)

Jotai atom utilities and integrations.

### Media (`src/media/`)

Media handling utilities.

## Testing

```bash
yarn test packages/common/infra  # Run infra tests
```
