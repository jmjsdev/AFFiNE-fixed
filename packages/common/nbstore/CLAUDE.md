# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/nbstore` (Notebook Store) is the storage abstraction layer providing unified APIs for document storage, sync, and blob management across different backends.

## Package Exports

```typescript
import { ... } from '@affine/nbstore';           // Core
import { ... } from '@affine/nbstore/idb';       // IndexedDB
import { ... } from '@affine/nbstore/sqlite';    // SQLite
import { ... } from '@affine/nbstore/cloud';     // Cloud sync
import { ... } from '@affine/nbstore/sync';      // Sync utilities
import { ... } from '@affine/nbstore/frontend';  // Frontend integration
```

## Architecture

### Directory Structure

```
src/
├── storage/       # Storage abstractions
├── sync/          # Sync engine
├── connection/    # Connection management
├── impls/         # Backend implementations
│   ├── idb/       # IndexedDB (browser)
│   ├── sqlite/    # SQLite (desktop)
│   ├── cloud/     # Cloud storage
│   └── broadcast-channel/  # Tab sync
├── frontend/      # Frontend integration
├── worker/        # Web worker support
│   ├── client.ts  # Worker client
│   └── consumer.ts # Worker handler
└── utils/
```

### Storage Types

- **DocStorage** - Yjs document storage
- **BlobStorage** - Binary blob storage (images, files)
- **SyncStorage** - Sync metadata

### Implementations

1. **IndexedDB** (`impls/idb/`) - Browser storage
2. **SQLite** (`impls/sqlite/`) - Desktop/Electron storage
3. **Cloud** (`impls/cloud/`) - Server sync via WebSocket
4. **BroadcastChannel** - Cross-tab synchronization

### Sync Engine (`sync/`)

Handles bi-directional sync between local and remote:
- Conflict resolution
- Offline queue
- Real-time updates via Socket.IO

### Web Worker

Heavy operations run in a web worker:
- `worker/client.ts` - Main thread client
- `worker/consumer.ts` - Worker thread handler

## Key Dependencies

- Yjs for CRDT documents
- `y-protocols` for sync protocol
- `rxjs` for reactive streams
- `idb` for IndexedDB wrapper
