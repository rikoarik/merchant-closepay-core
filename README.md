# Merchant Closepay Core (Member Base App)

React Native member app with multi-tenant config, modular plugins, and theming for Closepay V2.

## What’s inside
- React Native 0.82, TypeScript, React Navigation 7, Zustand, Axios, NativeWind.
- Core modules: auth, account, config, i18n, notification, security, theme, navigation.
- Core plugins: balance (ledger), payment (gateway, depends on balance).
- Domain plugins: catalog, order, reporting, and other verticals.
- App: `apps/member-base` with tenant-specific config and screens.

## Requirements
- Node.js 20+, npm
- Android: JDK 17+, Android Studio
- iOS (macOS): Xcode + CocoaPods

## Quick start
```bash
# 1) Install dependencies
npm install

# 2) Copy and adjust config
cp apps/member-base/config/app.config.template.ts apps/member-base/config/app.config.ts
# edit branding, services.api.baseUrl, enabledModules, etc.

# 3) (macOS) install pods
cd ios && pod install && cd ..

# 4) Run
npm start           # start Metro
npm run android     # run on Android emulator/device
npm run ios         # run on iOS simulator
```

## Configuration & theming
- Main config: `apps/member-base/config/app.config.ts`.
- Accent color: set `branding.primaryColor` (single source of truth). Use theme colors (e.g., `colors.primary`, `colors.surface`) for all interactive states—avoid hardcoded hex.
- Enable/disable plugins via config `enabledModules`.
- API base URL: `services.api.baseUrl`.

## Architecture (layers)
- **Core** (`packages/core`): generic services, hooks, components. No domain knowledge.
- **Plugins** (`packages/plugins`): domain-specific logic/UI; may depend on core and other plugins (payment → balance).
- **Apps** (`apps/*`): company/tenant-specific entry points, assets, and overrides.

## Project structure (short)
```
apps/member-base/          app entry + tenant config
packages/core/             shared modules (auth, config, i18n, theme, etc.)
packages/plugins/          balance, payment, catalog, order, reporting, ...
android / ios              native projects
assets/                    fonts, images
```

## Scripts
- Development: `npm start`, `npm run android`, `npm run ios`
- Android build: `npm run build:apk`, `npm run build:apk:debug`, `npm run build:apk:staging`, `npm run build:apk:prod`
- Tests: `npm test`, `npm run test:coverage`, `npm run test:e2e:android`, `npm run test:e2e:ios`
- Lint: `npm run lint`

## Troubleshooting
- Metro cache: `npm start -- --reset-cache`
- Android clean: `cd android && ./gradlew clean && cd ..`
- iOS pods (macOS): `cd ios && rm -rf Pods && pod install && cd ..`

## License
Private – Merchant Closepay V2
