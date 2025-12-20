# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/i18n` handles internationalization for AFFiNE using i18next and react-i18next.

## Commands

```bash
yarn affine i18n build   # Generate i18n types
yarn affine i18n dev     # Watch mode
```

## Architecture

### Files

- `src/index.ts` - Main exports
- `src/i18next.ts` - i18next configuration
- `src/react.ts` - React hooks and components
- `src/i18n.gen.ts` - Auto-generated types (do not edit)
- `src/resources/` - Translation JSON files
- `src/i18n-completenesses.json` - Translation completion stats

### Translation Files

Translations are in `src/resources/`:
```
resources/
├── en.json      # English (source)
├── zh-Hans.json # Simplified Chinese
├── zh-Hant.json # Traditional Chinese
├── fr.json      # French
├── de.json      # German
├── ja.json      # Japanese
├── ko.json      # Korean
└── ...
```

### Usage

```typescript
import { useI18n } from '@affine/i18n';

function Component() {
  const t = useI18n();
  return <span>{t['com.affine.welcome']()}</span>;
}
```

### Type Generation

The `build.ts` script uses `@magic-works/i18n-codegen` to:
1. Parse translation JSON files
2. Generate typed accessor functions in `i18n.gen.ts`
3. Provide compile-time type safety for translation keys

### Adding Translations

1. Add key to `src/resources/en.json`
2. Run `yarn affine i18n build`
3. Use the generated typed accessor

### Contributing Translations

See [i18n General Space](https://community.affine.pro/c/i18n-general) for contribution guidelines.
