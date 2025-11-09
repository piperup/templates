# @repo/typescript-config

This package exports shared TypeScript configurations used across the monorepo.

## What's inside

### `./base.json`

Base configuration for TypeScript projects including:

- Modern module system (ESNext with Bundler resolution)
- Declaration file generation with source maps
- Strict type checking enabled
- Isolated modules for better performance
- ES module interop
- Excludes `node_modules`

### `./react-library.json`

Configuration for React library packages, extending the base config with:

- JSX support with React 17+ transform (`react-jsx`)
- Inherits all base configuration settings

### `./vite.json`

Configuration for Vite-based applications, extending the base config with:

- ESNext target for modern JavaScript
- DOM library types included
- Source maps enabled
- JSON module resolution
- No emit (Vite handles compilation)
- Stricter unused variable/parameter checks
- Requires explicit return statements
- Excludes `node_modules` and `dist`

## Installation

### 1. Add to your app's dependencies

Add this package to your app's `package.json`:

```json
{
  "devDependencies": {
    "@repo/typescript-config": "workspace:*"
  }
}
```

Then run:

```sh
pnpm install
```

## Usage

### Using the base config

Create a `tsconfig.json` in your project root:

```json
{
  "extends": "@repo/typescript-config/base.json",
  "compilerOptions": {
    // Your custom compiler options
  },
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

### Using the React library config

For React library packages:

```json
{
  "extends": "@repo/typescript-config/react-library.json",
  "compilerOptions": {
    "outDir": "dist"
  },
  "include": ["src"]
}
```

### Using the Vite config

For Vite-based applications:

```json
{
  "extends": "@repo/typescript-config/vite.json",
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src"]
}
```

## Resources

- [TypeScript Configuration Reference](https://www.typescriptlang.org/tsconfig)
- [Turborepo TypeScript Guide](https://turbo.build/repo/docs/guides/tools/typescript)
