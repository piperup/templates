# @repo/eslint-config

Shared ESLint configurations using ESLint v9 flat config format.

## Configs

- `./base` — TypeScript projects (ESLint + TypeScript + Prettier + Turborepo)
- `./react-internal` — React projects (extends base + React + React Hooks)

## Installation

```json
{
  "devDependencies": {
    "@repo/eslint-config": "workspace:*"
  }
}
```

## Usage

### Base config

```js
import baseConfig from "@repo/eslint-config/base";

export default baseConfig;
```

### React config

```js
import reactConfig from "@repo/eslint-config/react-internal";

export default reactConfig;
```

### Extend with custom rules

```js
import baseConfig from "@repo/eslint-config/base";

export default [
  ...baseConfig,
  {
    rules: {
      "no-console": "warn",
    },
  },
];
```
