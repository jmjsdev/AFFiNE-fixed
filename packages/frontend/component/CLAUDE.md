# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/component` is the shared UI component library for AFFiNE. It provides reusable React components used across web, desktop, and mobile apps.

## Commands

```bash
yarn dev              # Start Storybook on port 6006
yarn build:storybook  # Build Storybook for deployment
```

## Architecture

### Directory Structure

```
src/
├── ui/           # Base UI primitives (button, input, modal, etc.)
├── components/   # Higher-level composed components
├── hooks/        # Shared React hooks
├── theme/        # Theme configuration
├── styles/       # Global styles
├── utils/        # Component utilities
└── lit-react/    # Lit-to-React integration utilities
```

### Component Exports

Components are exported via package.json exports:
- `@affine/component` - Main exports
- `@affine/component/theme` - Theme utilities
- `@affine/component/ui/*` - Individual UI components (e.g., `@affine/component/ui/button`)
- `@affine/component/*` - Higher-level components

### UI Components (`src/ui/`)

Base primitives built on Radix UI:
- `button`, `input`, `checkbox`, `radio`, `switch`
- `modal`, `popover`, `tooltip`, `menu`, `tabs`
- `avatar`, `skeleton`, `loading`, `progress`
- `date-picker`, `slider`, `table`
- `notification`, `toast`
- `dnd` (drag and drop via @atlaskit/pragmatic-drag-and-drop)

### Styling

- Uses `@vanilla-extract/css` for type-safe CSS
- Theme tokens from `@toeverything/theme`
- Responsive via CSS custom properties
- Dark mode support via `next-themes`

### Key Dependencies

- Radix UI for accessible primitives
- Jotai for component-level state
- Emotion for dynamic styles
- Lit for web components interop
