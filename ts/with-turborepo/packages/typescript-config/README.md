# @repo/typescript-config

Shared TypeScript configurations for monorepo packages.

## Configs

- `./base.json` — Base config with strict typing and ESNext modules
- `./react-library.json` — React libraries (extends base + JSX support)
- `./vite.json` — Vite apps (extends base + DOM types, no emit)

## Installation

```json
{
  "devDependencies": {
    "@repo/typescript-config": "workspace:*"
  }
}
```

## Usage

### Base config

```json
{
  "extends": "@repo/typescript-config/base.json",
  "include": ["src"]
}
```

### React library config

```json
{
  "extends": "@repo/typescript-config/react-library.json",
  "compilerOptions": {
    "outDir": "dist"
  },
  "include": ["src"]
}
```

### Vite config

```json
{
  "extends": "@repo/typescript-config/vite.json",
  "include": ["src"]
}
```
