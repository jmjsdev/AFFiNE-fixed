# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/graphql` contains auto-generated GraphQL client code for communicating with the AFFiNE server.

## Commands

```bash
yarn workspace @affine/graphql build  # Regenerate types from schema
```

## Architecture

### Code Generation

Uses GraphQL Code Generator (`@graphql-codegen/cli`):
- **Input**: Server's `schema.gql` (from `packages/backend/server/src/schema.gql`)
- **Output**: TypeScript types and operations in `src/`

### Configuration

- `codegen.yml` - GraphQL codegen configuration
- `export-gql-plugin.cjs` - Custom plugin for exports

### Generated Files

```
src/
├── index.ts           # Main exports
├── graphql/           # Generated operations
└── __tests__/
```

### Usage

```typescript
import { getUserQuery, createWorkspaceMutation } from '@affine/graphql';

// Use with your GraphQL client
const result = await client.query(getUserQuery);
```

## Updating

When the server schema changes:
1. Ensure server schema is up to date
2. Run `yarn workspace @affine/graphql build`
3. Commit generated changes

The schema is read from the server package, so schema changes automatically propagate on rebuild.
