# with-vite-react

React 19 + Vite + TypeScript app using shared monorepo packages.

## Development

```sh
# From monorepo root
pnpm install
pnpm dev  # http://localhost:5173
```

## Using shared packages

### Import UI components

```tsx
import { Header, Counter } from "@repo/ui";
import { Button } from "@repo/ui/components/ui/button";
```

### Import styles

In `src/style.css`:

```css
@import "tailwindcss";
@import "@repo/tailwind-config";
@source "../../../packages/ui/src/**/*.{ts,tsx}";
```

### Extend TypeScript config

In `tsconfig.json`:

```json
{
  "extends": "@repo/typescript-config/vite.json"
}
```

### Use ESLint config

In `eslint.config.js`:

```js
import reactConfig from "@repo/eslint-config/react-internal";

export default reactConfig;
```
