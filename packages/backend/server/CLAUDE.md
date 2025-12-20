# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/server` is the NestJS backend server providing GraphQL API, authentication, real-time sync, and cloud features.

## Commands

```bash
# Development (requires Docker services running)
yarn affine server dev         # Start dev server
yarn affine server init        # Run migrations + data migrations

# Testing
yarn workspace @affine/server test            # Run all tests (ava)
yarn workspace @affine/server test:copilot    # Run copilot tests only
yarn workspace @affine/server e2e             # Run e2e tests

# Database
yarn affine server prisma studio   # Open Prisma Studio (DB GUI)
yarn affine server prisma migrate  # Run migrations
yarn affine server seed            # Seed database

# Production
yarn workspace @affine/server build  # Bundle for production
```

## Architecture

### Entry Points

- `src/index.ts` - Main entry, routes to CLI or server based on `env.flavors.script`
- `src/server.ts` - Server bootstrap
- `src/cli.ts` - CLI commands (data migrations, etc.)

### Core Modules (`src/core/`)

NestJS modules providing main functionality:

- `auth/` - Authentication (email/password, OAuth, magic links)
- `user/` - User management
- `workspaces/` - Workspace CRUD, membership
- `doc/` - Document operations
- `sync/` - Real-time sync via WebSocket
- `storage/` - Blob storage (S3, local)
- `quota/` - Usage quotas and limits
- `permission/` - Access control
- `mail/` - Email sending
- `notification/` - User notifications
- `features/` - Feature flags
- `comment/` - Document comments
- `config/` - Runtime configuration

### Data Layer

- **Prisma ORM** - Database access (`prisma/schema.prisma`)
- **PostgreSQL** - Primary database (with pgvector for embeddings)
- **Redis** - Caching, sessions, Socket.IO adapter

### API

- **GraphQL** - Primary API (`schema.gql` auto-generated)
- **REST** - Blob upload/download, OAuth callbacks
- **WebSocket** - Real-time sync (Socket.IO)

### Plugins (`src/plugins/`)

Optional features enabled by config:
- Copilot (AI features)
- Payment (Stripe integration)
- OAuth providers

### Key Patterns

**Resolvers**: GraphQL resolvers in `**/resolver.ts` files
**Services**: Business logic in `**/service.ts` files
**Guards**: Auth/permission guards in `**/guard.ts` files

### Test Users (dev mode)

- `dev@affine.pro` / `dev` (default user)
- `pro@affine.pro` / `pro` (pro features)
- `team@affine.pro` / `team` (team workspace)
