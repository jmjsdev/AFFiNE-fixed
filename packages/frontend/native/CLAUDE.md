# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/native` contains native Rust modules compiled to Node.js bindings via NAPI-RS. Used by the Electron app for performance-critical operations.

## Commands

```bash
# Build release binary
yarn affine @affine/native build

# Build debug binary
yarn workspace @affine/native build:debug

# Run tests
yarn workspace @affine/native test
```

## Architecture

### Rust Source (`src/`)

- `lib.rs` - Main entry, exports to Node.js
- `hashcash.rs` - Hashcash implementation

### NAPI-RS

Uses NAPI-RS to create Node.js native addons:
- Compiles Rust to platform-specific binaries
- Generates TypeScript type definitions
- Supports multiple targets (macOS, Linux, Windows, arm64, x64)

### Target Platforms

```
x86_64-apple-darwin      # macOS Intel
aarch64-apple-darwin     # macOS Apple Silicon
x86_64-unknown-linux-gnu # Linux x64
aarch64-unknown-linux-gnu # Linux arm64
x86_64-pc-windows-msvc   # Windows x64
aarch64-pc-windows-msvc  # Windows arm64
```

## Development

### Prerequisites

1. Rust toolchain: https://rustup.rs/
2. For cross-compilation, install target: `rustup target add <target>`

### Building

The build outputs platform-specific binaries:
- `affine.darwin-x64.node`
- `affine.darwin-arm64.node`
- `affine.linux-x64-gnu.node`
- etc.

### Testing

Tests are in `__tests__/*.spec.mts` using AVA.
