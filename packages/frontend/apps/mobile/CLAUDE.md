# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this directory.

## Overview

`@affine/mobile` is the mobile web application, optimized for touch interfaces and mobile browsers.

## Architecture

Similar to `@affine/web`, this is a thin wrapper around `@affine/core` with mobile-specific:
- Viewport configuration
- Touch event handling
- Mobile UI adaptations

### Mobile-Specific Code

Mobile-specific features in `@affine/core` are in:
- `packages/frontend/core/src/mobile/` - Mobile views and components

### Relationship to Native Apps

For native mobile apps (iOS/Android):
- `packages/frontend/apps/ios/` - iOS Capacitor app
- `packages/frontend/apps/android/` - Android Capacitor app

These wrap the mobile web build with native capabilities via Capacitor.
