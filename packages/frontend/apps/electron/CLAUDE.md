# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/electron` is the desktop application built with Electron, wrapping the AFFiNE web app with native features.

## Commands

```bash
# Development
yarn affine @affine/electron dev          # Start with dev server
yarn affine @affine/electron dev:prod     # Start with production build

# Build
yarn affine @affine/electron build        # Build layers
yarn affine @affine/electron generate-assets  # Generate static assets

# Package & Make
yarn affine @affine/electron package      # Package app
yarn affine @affine/electron make         # Create installers (Mac/Linux)
yarn affine @affine/electron make-squirrel  # Windows Squirrel installer
yarn affine @affine/electron make-nsis    # Windows NSIS installer
```

## Architecture

### Process Model

```
src/
├── main/          # Main process (Node.js)
│   ├── windows-manager/  # Window lifecycle
│   ├── updater/         # Auto-update
│   └── exposed.ts       # APIs exposed to helper
├── helper/        # Helper process (sandboxed Node.js)
│   └── exposed.ts       # APIs exposed to renderer
├── preload/       # Preload scripts (bridge main↔renderer)
│   ├── electron-api.ts  # Electron API bridge
│   └── shared-storage.ts
└── shared/        # Shared between processes
```

### IPC Communication

Uses `async-call-rpc` for type-safe IPC:
- Main ↔ Helper: Direct Node.js communication
- Helper ↔ Renderer: Via preload scripts
- Renderer uses `@affine/electron-api` for typed access

### Key Features

- **Native SQLite**: Uses `@affine/native` for local storage
- **Auto-update**: Via `electron-updater`
- **Deep links**: Handles `affine://` protocol
- **Window management**: Multi-window support

### Build Process

1. Build native modules: `yarn affine @affine/native build`
2. Build core web app
3. Build electron layers: `yarn affine @affine/electron build`
4. Generate assets: `yarn affine @affine/electron generate-assets`
5. Package: Requires yarn config changes (see `docs/building-desktop-client-app.md`)

### Electron Forge

Uses Electron Forge for packaging:
- `forge.config.js` - Forge configuration
- Makers: DMG, Squirrel, NSIS, AppImage, Flatpak, DEB, ZIP
