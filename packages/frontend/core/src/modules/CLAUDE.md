# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

This directory contains all feature modules for the AFFiNE application. Each subdirectory is a self-contained module following the DI framework pattern.

## Module Structure

Each module typically contains:

```
<module>/
├── index.ts           # Exports + configure*Module(framework) function
├── entities/          # Entity classes (per-instance stateful objects)
├── services/          # Service classes (singleton business logic)
├── stores/            # Store classes (data access layer)
├── scopes/            # Scope definitions (DI boundaries)
├── providers/         # Abstract interfaces
├── views/             # React components
├── events.ts          # Framework events
└── types.ts           # TypeScript types
```

## Key Modules

### Core
- `workspace/` - Workspace management, creation, storage
- `doc/` - Document CRUD, properties
- `editor/` - BlockSuite editor integration
- `storage/` - Local storage (GlobalState, GlobalCache)

### UI/UX
- `workbench/` - Main layout, tabs, panels
- `dialogs/` - Modal dialog system
- `peek-view/` - Peek/preview views
- `quicksearch/` - Quick search (Cmd+K)
- `navigation/` - Routing, navigation

### Cloud
- `cloud/` - Cloud sync, server communication
- `share-doc/` - Document sharing
- `permissions/` - Access control

### Features
- `favorite/` - Favorites
- `collection/` - Collections
- `tag/` - Tags
- `journal/` - Daily journal
- `ai-button/` - AI features
- `comment/` - Comments

## Creating a New Module

1. Create directory: `src/modules/<name>/`
2. Create `index.ts` with `configure*Module(framework)` function
3. Register in app bootstrap
4. Follow existing patterns for entities/services/stores

## Common Patterns

### LiveData for Reactive State
```typescript
class MyService extends Service {
  items$ = new LiveData<Item[]>([]);

  addItem(item: Item) {
    this.items$.next([...this.items$.value, item]);
  }
}
```

### Entity with Scope
```typescript
const DocScope = Scope('doc');

class Doc extends Entity {
  constructor(private readonly scope: DocScope) {}
}
```

### Store for Data Access
```typescript
class DocsStore extends Store {
  getDoc(id: string) { /* ... */ }
  watchDocs() { return this.livedata$; }
}
```
