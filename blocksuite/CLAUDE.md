# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

BlockSuite is AFFiNE's collaborative editing framework. It provides a block-based editor with CRDT synchronization (Yjs), supporting both document and whiteboard (edgeless) modes.

## Structure

```
blocksuite/
├── framework/     # Core framework packages
│   ├── global/    # @blocksuite/global - Shared utilities, DI, types
│   ├── store/     # @blocksuite/store - Document model, Yjs integration
│   ├── std/       # @blocksuite/std - Editor standards, selection, clipboard
│   └── sync/      # @blocksuite/sync - Sync providers
├── affine/        # AFFiNE-specific blocks and features
│   ├── all/       # @blocksuite/affine - Meta package exporting everything
│   ├── blocks/    # Block implementations (paragraph, list, image, etc.)
│   ├── components/# Shared UI components (toolbar, menus, etc.)
│   ├── data-view/ # Database/table view
│   ├── fragments/ # UI fragments (outline, doc-title, etc.)
│   ├── gfx/       # Graphics elements (shapes, connectors, mindmap)
│   ├── inlines/   # Inline elements (links, mentions, footnotes)
│   ├── widgets/   # Editor widgets (slash-menu, toolbar, drag-handle)
│   ├── model/     # Block models
│   ├── rich-text/ # Rich text editing
│   └── shared/    # Shared utilities
├── playground/    # Development playground
└── integration-test/
```

## Key Concepts

### Blocks

The document is a tree of blocks. Each block type has:
- **Model** - Data schema (extends `BlockModel`)
- **View** - Lit element rendering the block
- **Store** - Block-specific services

Block types: `paragraph`, `list`, `code`, `image`, `database`, `table`, `embed`, `note`, `surface` (whiteboard), etc.

### Store (`@blocksuite/store`)

- `Doc` - Yjs document wrapper
- `Workspace` - Collection of docs
- `Block` - Block instance in the tree
- `Schema` - Block schema definitions

### Std (`@blocksuite/std`)

- `EditorHost` - Main editor container
- `Selection` - Selection management
- `Clipboard` - Copy/paste handling
- `Command` - Command system
- `Event` - Event handling

### Graphics (Edgeless Mode)

The `gfx/` packages provide whiteboard elements:
- `shape` - Rectangles, circles, etc.
- `connector` - Lines connecting elements
- `brush` - Freehand drawing
- `mindmap` - Mind map structures
- `text` - Edgeless text boxes

### Widgets

UI overlays in the editor:
- `slash-menu` - "/" command menu
- `toolbar` - Formatting toolbar
- `drag-handle` - Block drag handle
- `linked-doc` - Document linking UI

## Commands

```bash
# Run tests
yarn workspace @blocksuite/affine test

# Build
yarn workspace @blocksuite/affine build
```

## Lit Components

BlockSuite uses Lit for web components. Views extend Lit's `LitElement` with custom decorators for block binding.
