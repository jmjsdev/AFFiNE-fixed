# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/server-native` contains native Rust modules for the backend server, compiled via NAPI-RS.

## Commands

```bash
# Build release binary
yarn affine @affine/server-native build

# Build debug binary
yarn workspace @affine/server-native build:debug

# Run tests
yarn workspace @affine/server-native test

# Run benchmarks
yarn workspace @affine/server-native bench
```

## Architecture

### Rust Source

Located in `src/` (Rust files), providing performance-critical server operations:
- Token operations (tiktoken-like functionality)
- Cryptographic operations
- Other CPU-intensive tasks

### NAPI-RS

Uses NAPI-RS to compile Rust to Node.js native addons:
- Output: `server-native.node` binary
- TypeScript types in `index.d.ts`

### Target Platforms

```
aarch64-apple-darwin       # macOS Apple Silicon
x86_64-apple-darwin        # macOS Intel
aarch64-unknown-linux-gnu  # Linux arm64
x86_64-unknown-linux-gnu   # Linux x64
aarch64-pc-windows-msvc    # Windows arm64
x86_64-pc-windows-msvc     # Windows x64
```

## Development

### Prerequisites

1. Rust toolchain
2. For specific targets: `rustup target add <target>`

### Testing

Tests in `__tests__/*.spec.js` using Node.js built-in test runner.

### Benchmarks

Performance benchmarks in `benchmark/index.js`.
