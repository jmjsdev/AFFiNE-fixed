# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

This directory contains E2E and integration tests for AFFiNE using Playwright.

## Structure

```
tests/
├── kit/                    # @affine-test/kit - Shared test utilities
├── affine-local/           # Local-only (no server) E2E tests
├── affine-cloud/           # Cloud/server E2E tests
├── affine-cloud-copilot/   # AI copilot E2E tests
├── affine-desktop/         # Electron desktop E2E tests
├── affine-desktop-cloud/   # Desktop + cloud E2E tests
├── affine-mobile/          # Mobile E2E tests
├── blocksuite/             # BlockSuite integration tests
└── fixtures/               # Test fixtures
```

## Commands

```bash
# Run local E2E tests
yarn workspace @affine-test/affine-local e2e

# Run cloud E2E tests (requires server running)
yarn workspace @affine-test/affine-cloud e2e

# Run desktop E2E tests
yarn workspace @affine-test/affine-desktop e2e

# Run mobile E2E tests
yarn workspace @affine-test/affine-mobile e2e

# Install Playwright browsers (first time)
npx playwright install
```

## Test Kit (`tests/kit/`)

Shared utilities for tests:

- `src/playwright.ts` - Playwright test utilities
- `src/electron.ts` - Electron testing helpers
- `src/mobile.ts` - Mobile testing helpers
- `src/utils/` - Common test utilities
- `src/bs/` - BlockSuite testing helpers

## Writing Tests

Tests use Playwright Test framework:

```typescript
import { test, expect } from '@playwright/test';

test('should create new page', async ({ page }) => {
  await page.goto('/');
  // ...
});
```

## Prerequisites

1. For local tests: Start the dev server (`yarn dev`)
2. For cloud tests: Start server + Docker services
3. For desktop tests: Build electron app first
