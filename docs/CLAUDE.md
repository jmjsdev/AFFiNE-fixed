# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

This directory contains development documentation for AFFiNE.

## Key Documents

- `BUILDING.md` - How to build the web app
- `building-desktop-client-app.md` - Desktop (Electron) build process
- `developing-server.md` - Server development setup
- `CONTRIBUTING.md` - Contribution guidelines (redirects to online docs)
- `contributing/tutorial.md` - Codebase tutorial for new contributors

## Quick Links

### Build Commands
```bash
yarn install                          # Install dependencies
yarn affine @affine/native build      # Build frontend native
yarn affine @affine/server-native build  # Build server native
yarn dev                              # Start web dev server
yarn affine server dev                # Start backend server
```

### Server Setup
Requires Docker for postgres, redis, mailhog:
```bash
docker compose -f .docker/dev/compose.yml up
yarn affine server init
```

### Desktop Build
See `building-desktop-client-app.md` for the multi-step process.

## Contributing

For detailed contribution guidelines, see https://docs.affine.pro/docs/contributing
